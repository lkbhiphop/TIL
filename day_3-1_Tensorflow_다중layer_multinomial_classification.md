# Tensorflow 다중신경망

Tensorflow의 기초부분에 대한 이야기는 일단 생략하고 오늘 배운 것 중 저를 멘붕에 빠트렸던(?) 다중 신경망에 정리해보았습니다.

저는 Tensorflow단계를 나누어 실행하려 했습니다.

단계를 나누어 checklist를 만들기 위해서입니다.

(제가 사용한 코드는 deeplearning repository에 있으니 참고 부탁드립니다.)

### tensorflow 구축(그래프 구축) - 1~7단계

- #### 1단계 - 데이터 load와 train data, label data 나누기

  ```python
  import tensorflow as tf
  import numpy as np
  from tensorflow.examples.tutorials.mnist import input_data
  import random
  import matplotlib.pyplot as plt
  mnist = input_data.read_data_sets("MNIST_data/",one_hot = True) 
  x_data = mnist.train.images # train
  y_data = mnist.train.labels	# label
  ```

위의 과정은 tensorflow의 내장되어있는 mnist 파일을 활용했습니다.

만약 train과 label이 나누어져 있지 않다면 slicing을 통해 나누면 됩니다.

- #### 2단계 - x_data와 y_data를 담을 그릇(placeholder) 만들기

```python
X = tf.placeholder(tf.float32,shape = [None,784])
Y = tf.placeholder(tf.float32,shape = [None,10])
```

X, Y라는 변수에 x_data와 y_data를 담을 수 있는 placeholder(tensor)를 만듭니다.

여기서 주의할 점은 `x_data.shape	`을 통해 shape을 확인해야한다는 점인데요 데이터가 들어가야할 그릇이기때문에 그 shape이나 차원이 일치해야합니다.

- #### 3단계 - weight에 대한 변수 만들기(without hidden layer)

```python
W = tf.Variable(tf.random_normal([784,10]))
b = tf.Variable(tf.random_normal([10]))
```

위 코드는 하나의 layer를 만들 때 쓰입니다. w가 하나라는 의미는 아닙니다. 왜냐하면 이미 위의 데이터에서 matrix 형태로 x 데이터를 받았기 때문에 이와 곱해서 weight를 계산한 변수므로 아래와 같은 모양으로 w를 생성하는 겁니다.

![w](https://user-images.githubusercontent.com/13254880/47782789-66fa6280-dd44-11e8-8aa9-f9ba077e3624.png)

또한 예측해야 할 값이 10개의 label이기 때문에 각 label에 맞는 w와 b를 만들어줘야하기 때문에 w는 784개의 w1..wn이 10개가 생성되고, b는 각 label별로 10개가 변수로 생성되는 겁니다.  

(b 그림은 생략)

![23361e50579e35d21e](https://user-images.githubusercontent.com/13254880/47782753-56e28300-dd44-11e8-91ad-c0a155c1ebbd.png)

성킴 교수님의 강의노트를 빌리면 가장 왼쪽에 있는 matrix를 생성한다고 생각하시면 됩니다. 이러한 숫자들을 random_normal()로 정규분포를 따르는 숫자로 내부 matrix를 채우는 거죠 

변수 초기화 방법 같은 경우는 다양한 방법이 있지만, 가장 보편화되고 쉬운 방법을 사용했습니다.



X를 가로로 해야 matrix곱이 가능하기 때문에 이러한 방식으로 placeholder와 Variable을 생성했습니다.

- #### 3단계 - weight에 대한 변수 만들기(with hidden layer)

```python
W1 = tf.Variable(tf.random_normal([784,256]))
b1 = tf.Variable(tf.random_normal([256]))
layer1 = tf.nn.relu(tf.matmul(X,W1)+b1)

W2 = tf.Variable(tf.random_normal([256,256]))
b2 = tf.Variable(tf.random_normal([256]))
layer2 = tf.nn.relu(tf.matmul(layer1,W2)+b2)

W3 = tf.Variable(tf.random_normal([256,256]))
b3 = tf.Variable(tf.random_normal([256]))
layer3 = tf.nn.relu(tf.matmul(layer2,W3)+b1)

W4= tf.Variable(tf.random_normal([256,10]))
b4 = tf.Variable(tf.random_normal([10]))
logits = tf.matmul(layer3,W4) + b4
```

드디어 딥러닝의 꽃이자 저를 멘붕에 빠트렸던 다중layer를 통한 y값 예측입니다.

먼저 Hidden layer를 사용하는 이유는 x_data에 대한 정보를 더 세부적으로 나누어 y값을 예측하기 위함이라고 생각하면 편할 것 같습니다.

weight의 값을 조절하여 cost를 최소화 시키는 딥러닝에서 x값에 대한 정보가 늘어나고 weight가 더 많이 늘어난다면 더 정확한 예측이 가능할 것입니다.

그럼 이러한 과정의 가장 핵심적인 개념인 **오차역전파** 라는 개념을 간단히 설명드리겠습니다.

1. 순전파(forward)방식으로 y값을 구합니다. 

2. 구한 y값을 실제 예측값과 비교하여 loss를 구합니다.
3. chain rule을 이용하여 y값에 끼치는 각 weight의 영향력(가중치)를 구합니다.
4. 이러한 영향력을 기반으로 input방향(역전파)으로 오차를 보내면서 가중치를 고려하여 weight를 조절합니다.

![default](https://user-images.githubusercontent.com/13254880/47782646-1256e780-dd44-11e8-8e33-6ac980cd1d66.PNG)

위와 같은 과정을 통해 저희는 더 정교하게 세부적으로 weight값을 조절할 수 있고 더 정확한 y값을 예측할 수 있는 것입니다.



사실 말하면서도 이해가 정확히 가지 않은 부분들이 있기 때문에 더 학습한 후 수정하도록 하겠습니다. ㅎㅎ

- #### 4단계 - hypothesis 생성하기(y값을 생성하는 식)

```python
hypothesis = tf.nn.softmax(logits)
```

여기서는 multinomial classification이기 때문에 y값을 예측하는 식에 softmax라는 메쏘드를 통해 최소값으로 향하는 convex한 모양을 만들어 줍니다.

이래야 cost를 줄일 때 최소값으로 갈 수 있기 때문입니다.

- #### 5단계 - cost 생성하기(어떠한 기준으로 학습할 것인지)

```python
cost = tf.reduce_mean(tf.nn.softmax_cross_entropy_with_logits(logits = logits, labels = Y))

```

위의 cost생성은 어떠한 기준으로 학습을 진행할지에 대한 이야기 입니다. 

위에서 구분을 위한 선(tf.matmul(layer3,W4) + b4)을 그었고, 이 선이 데이터를 잘 표현하는지에 대해 평가하는 기준이 바로 cost_functino입니다. 

여기서 이 cost를 minimize하는 w와 b를 찾는 과정이 바로 딥러닝인거죠 호호

- #### 6단계 - optimizer(어떠한 방식으로 최소의 기준(cost)를 다가갈지)

```python
optimizer = tf.train.AdamOptimizer(learning_rate=0.01)
```

이 단계는 cost_function이라는 기준을 작게 만들기 위해 무슨 방법을 사용할지에 대한 이야기입니다. 여기서 learning_rate는 학습률을 이야기합니다.

학습률에 대한 이야기는 얼마만큼(크게,작게) cost를 찾기위해 움직인다는 뜻입니다. 

**여기서 궁금한 점은 학습률은 언제가 가장 좋을까요?** 

답은 !!!! 데이터마다 다 다릅니다. ㅎㅎ 보통 0.1부터 0.001사이의 값으로 쓰는데요 

복불복과 같이 알 수 없기 때문에 시나리오를 정해서 직접 실행해야합니다... 스마트한 노가다라고 할 수 있죠

- #### 7단계 - train(그래프 그려서 찾기)

```python
train = optimizer.minimize(cost)
```

사실 위의 단계와 함께 진행해도되지만, 실제로 cost를 최소화하기 위한 optimizer를 위한 그래프 단계를 따로 했습니다.



여기까지가 그래프 생성단계입니다:)

엄청 복잡한 거 같지만

1. 데이터 load, train_data, label 나누기
2. 데이터그릇(placeholder)
3. 변수(Weight) (one-layer/multi layer)
4. hypothesis(예측을 위한 선 긋기)
5. cost(선이 잘그어졌나~ 평가하는 기준)
6. optimizer(어떤 방법으로 cost를 줄여가려고?)
7. train으로 그래프 직접 그리기 입니다!!



### tensorflow session을 통한 실행

이제부터는 실제 세션을 열어서 딥러닝모델을 생성할 건데요 

epoch와 batch를 이용해 더 빠르게 정확한 모델을 생성하겠습니다.

그럼 다시 8단계 입니다.

- #### 8단계 - 세션열기  +  변수 초기화하기

```python
sess = tf.Session()
sess.run(tf.global_variables_initializer())
```

말 그대로 세션을 열고, 변수를 움직일 준비를 시킨거죠 (initializer)

- #### 9단계 - epoch과 batch를 이용한 모델학습

```python
training_epoch = 15
batch_size = 100
for epoch in range(training_epoch):
    total_batch = int(mnist.train.num_examples/batch_size)
# 한 세대를 batch_size로 나누면 총 배치횟수를 알수 있다. 
    avg_cost = 0
# epoch마다 cost 평균을 구해서 보여줘야하므로 batch for문 위에    # avg_cost=0으로 초기화해준다.
    for i in range(total_batch):
        batch_xs, batch_ys = mnist.train.next_batch(batch_size)
# mnist.train.next_batchs는 데이터를 slicing을 해서 
# x데이터와 y데이터를 나눠 반환한다.
        c, _ = sess.run([cost,train], feed_dict = {X:batch_xs,Y:batch_ys})
        avg_cost += c/total_batch
# cost를 다 더해서 total_Batch로 나눈것과 같은 효과
# (즉 모든 cost 더한 후 평균낸거와 같은 값을 가짐)
    print("Epoch",epoch, "Cost",avg_cost )
```

epoch은 세대를 뜻합니다. 1세대, 2세대와 같이 전체 데이터를 이야기 하는 것입니다.

batch_size는 한 세대(전체 데이터셋 한바퀴)를 돌 때 몇 개씩 볼 것인지에 대한 이야기 입니다.

그렇기 때문에 batch_size로 train데이터의 숫자를 나누면 한 세대를 돌기 위해 batch_size로 몇번 반복해야하는지 나오는 것입니다.

여기서는 

**55000개가 1 epoch**으로 전체 사이즈를 이야기하고,

**100개가 batch_size**으로 total_batch(총 batch해야할 수)는 550번입니다.

이러한 epoch과 batch를 하는 이유는 2가지 입니다.

1. w값을 정교하게 업데이트할 수 있습니다.

55000개를 학습하여 1번 w를 업데이트하는 것보다는 550번에 나누어 w를 업데이트하고 이를 15epoch한다면 당연하 w는 더 정교해지고 cost는 작아질것입니다. 예시는 아래와 같습니다. ㅎㅎ

![epoch](https://user-images.githubusercontent.com/13254880/47784854-50570a00-dd4a-11e8-9547-9e16f5bd1c0a.PNG)

2. 속도가 엄청나게 차이난다.

내부적으로는 아직 정확히 모르지만 epoch과 batch를 통해 더 빠른 연산을 할 수 있습니다. 정말 큰 차이를 보입니다. 데이터가 작으면 모르겠지만 크다면 꼭 써야한다고 생각합니다.

- #### 10단계 - test upload + 정확도 검사

```python
x_test = mnist.test.images
y_test = mnist.test.labels
is_correct = tf.equal(tf.argmax(hypothesis,1),tf.argmax(Y,1))
accuracy = tf.reduce_mean(tf.cast(is_correct, tf.float32))
sess.run(accuracy, feed_dict={X:x_test,Y:y_test})

```

test 데이터를 업로드한 후,

tf.argmax(예측값,axis = 1)을 이용해서 가장 큰 값의 index

tf.argmax(실제label, axis = 1)을 이용해서 실제 label의 index

여기서 axis = 1은 [[0., 0., 0., ..., 1., 0., 0.] ]이렇게 가장 바깥에서 1번째(0부터시작)중에 가장 큰 argument를 뽑아내기 위한 parameter입니다.

이 두 가지 값을 tf.equal()로 boolean타입으로 받습니다.

이걸 float값으로 캐스팅하면 같으면 1 다르면 0이고, 이를 평균내면 정확도가 나옵니다

ex) 1이 60개 0이 40개 60/(60+40)  이므로 정확도가 나옵니다.

단, accuracy 또한 하나의 tensor이기 때문에 sess.run을 통해 구현해야하고, feed_dict로 데이터를 넣어주면됩니다.

저는 이렇게 1~10단계를 통해서 딥러닝 다중layer를 통한 multinomial classification을 배웠습니다. 

내용은 더욱 꾸준히 보강하도록하겠습니다.