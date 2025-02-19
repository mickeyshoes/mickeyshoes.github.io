---
layout: post
title:  "Jetson Nano benchmark"
date:   2019-06-27 02:11:00
last_modified_at:  2019-06-27 02:11:00
excerpt: "이번엔 Jetson Nano를 이용하여 benchmark를 진행하고자 한다. 이번에 무슨 사업을 벤치마크 하러 어디를 간다더라 이런 이야기를 다들 많이 들어 봤을 것이다."
categories: lab
tags:  Jetson Nano
image:
  feature: mickey-stupid.jpg
  topPosition: 0px
bgContrast: dark
bgGradientOpacity: darker
syntaxHighlighter: no
---

Jetson Nano benchmark
--

이번엔 Jetson Nano를 이용하여 benchmark를 진행하고자 한다.

이번에 무슨 사업을 벤치마크 하러 어디를 간다더라 이런 이야기를 다들 많이 들어 봤을 것이다.

우리는 저 대화에 자연스럽게 낄 지혜가 필요하다.

benchmark가 무슨 뜻인지부터 한번 살펴보자.

<div class="img img--fullContainer img--8xLeading" style="background-image: url({{ site.baseurl_posts_img }}meaning_of_benchmark01.png);"></div>

출처 - 네이버 사전

그렇다. "기준" 이라는 뜻이었다.  

(칵테일을 먼저 떠올렷다면 무슨 맛인지 후기를 남겨주길 바란다.)

기준 이라는 말은 뭔가 우리가 생각했던 뜻과 좀 동떨어져 있다.

이번엔 구선생님에게 물어보자.

구선생님께서 말씀하시길,

### 경영적인 측면 :
경쟁 업체의 경양방식을 면밀히 분석하여 자사의 경영과 생산에 응용하고 따라잡는 경영 전략.

### 컴퓨팅적 측면 :
컴퓨터의 부품 등의 성능을 프로그램을 이용하여 비교, 평가하여 점수를 내는 결과

라고 한다. 역시 구선생님이다.

그렇다면 경영적인 측면은 교양있는 대화에서 써 먹고, 우리는 **컴퓨팅적 측면**에서 Jetson Nano를 씹고 뜯고 맛보고 즐겨보자.






***

# Benchmark

<div class="img img--fullContainer img--10xLeading" style="background-image: url({{ site.baseurl_posts_img }}jetson_nano-deep_learning_inference_perf-chart.png);"></div>

출처 - [nvidia developer](https://developer.nvidia.com/embedded/jetson-nano-dl-inference-benchmarks)  


사실 Jetson Nano의 Benchmark는 Jetson의 판매사인 nvidia에서 친절하게 작성하여 그래프로 그려주었다.

그렇다면 왜 하려는것인가?

그렇다. 의심병이다.

nvidia측의 상술에 넘어가면 안된다. 일단 의심부터 하고본다.

그럼 바로 benchmark를 시작해보자.

의심이 간다고는 했지만, benchmark 방식은 nvidia측에서 제공한 지시를 따라서 할 것이다.

자세한 설명을 원한다면 [링크](https://developer.nvidia.com/embedded/jetson-nano-dl-inference-benchmarks)를 참고하면 되겠다.

영어와 친하지 않아서 직접 설명을 못해주기 때문에 그런것은 절대 아니다.

전부 benchmark를 해보진 않을 것이고 몇개만 추려서 제시한 자료와 맞는지만 확인해보자.

(benchmark는 TensorRT와 함께하고, **fp는 16**(반정밀)으로, **batch는 1**을 기준으로 한다.
)

betchmark를 하기 전에, nvidia측에서 권장하는 power supply를 맞추기 위해서
Jetson을 10W perfomance mode로 해주어야 한다.

Jetson의 power mode 에는 0과 1이 있는데, 0은 10W 1은 5W이다.

5W 모드로 실행을 할 경우 benchmark를 하는 도중에 종료되거나, 시스템이 불안정해 질 수 있다고 하니 주의하자.

<blockquote class="u--startsWithDoubleQuote">sudo nvpmodel -m 0<br>
sudo jetson_clocks</blockquote>

자 그럼 benchmark의 결과를 비교해보자.

각 benchmark에 이용된 model들은 다른 포스팅에서 설명 할 예정이다.

평균값은 소숫점 4째자리까지 표현하였고, 반올림을 하여 나타낸다.

* SSD-mobilenet-V2 (300 x 300)
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}SSD-Mobilenet-V2.png);"></div>
평균값 : 26.2355ms / 38.4615fps

* ResNet 50
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}ResNet-50.png);"></div>
평균값 : 27.8128ms / 35.7143fps

* Inception V4
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}Inception_V4.png);"></div>
평균값 : 95.9434ms / 10.4167fps

* U-Net Segmentation
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}U-Net_Segmentation.png);"></div>
평균값 : 64.4632ms / 15.625fps

* Pose Estimation
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}Pose_Estimation.png);"></div>
평균값 : 87.3721ms / 11.4943fps

* Super Resolution
<div class="img img--fullContainer img--7xLeading" style="background-image: url({{ site.baseurl_posts_img }}Super_Resolution.png);"></div>
평균값 : 67.5191ms / 14.7059fps

* Tiny YOLO v3 (단일 측정)
<div class="img img--fullContainer img--14xLeading" style="background-image: url({{ site.baseurl_posts_img }}tiny-yolo3.png);"></div>
평균값 : 56.7769ms / 17.5439fps

숫자는 머리가 너무 어지러우니, 측정한 값들을 보기 좋게 해보자.
<div class="img img--fullContainer img--14xLeading" style="background-image: url({{ site.baseurl_posts_img }}jetson_benchmark_graph.png);"></div>

측정한 그래프의 fps와 nvidia측에서 제공한 benchmark 그래프와 비교해보자.

비슷하다. 이래서 대기업 대기업 하나 싶다.

결론 - 의심하지 말자.
