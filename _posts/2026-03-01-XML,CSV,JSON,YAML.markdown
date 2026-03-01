---
layout: post
title: "XML,CSV,JSON,YAML 포맷 설명"
date: 2026-03-01 14:43:20 +0900
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img:  # Add image post (optional)
---
**"XML (eXtensible Markup Language)"**

XML은 말 그대로 확장 가능한 마크업 언어입니다. 마크업 언어란 문서의 형식이나 데이터의 구조를 나타내기 위해 태그를 사용하는 언어를 뜻합니다. HTML과 비슷해 보이지만, 사용자가 직접 태그를 정의할 수 있다는 점이 다릅니다.
{% highlight xml %}
<User>
    <Name>Seonggyun</Name>
    <Role>Developer</Role>
</User>
{% endhighlight %}
Python에서 XML을 파싱할 때는 주로 xml.etree.ElementTree 라이브러리를 사용합니다. 이때 특정 태그를 찾을 때 오타가 나거나 경로가 틀리면 None이 반환되어 에러가 발생할 수 있으니 예외 처리에 주의해야 합니다.

**"CSV (Comma Separated Values)"**

CSV는 이름 그대로 **쉼표(,)**로 데이터를 구분하는 방식입니다. 가장 단순하고 용량이 작다는 장점이 있지만, 데이터 하나하나에 대한 구체적인 태그(설명)가 없다는 단점도 있습니다.
단순히 쉼표로 구분되어 있다 보니, 각 열이 무엇을 의미하는지 파악하려면 파일의 최상단에 있는 헤더(Header) 정보를 확인해야 합니다.

{% highlight csv %}
id, x_center, y_center, width, height
0, 0.5, 0.5, 0.2, 0.3
{% endhighlight %}

Object Detection 모델인 YOLO의 라벨(txt 포맷이지만 구조는 유사함)을 보면 class_id, x, y, w, h처럼 최소한의 정보만 담고 있는 것을 볼 수 있습니다. 반면, 다음에 설명할 JSON 기반의 COCO Dataset format은 이미지 정보, 카테고리, 서브 클래스 등 훨씬 방대한 정보를 계층적으로 포함하고 있죠.

**"JSON (JavaScript Object Notation)"**

JSON은 데이터를 Key-Value(키-값) 쌍으로 나타내며, 현대 개발 환경에서 가장 표준적으로 사용됩니다. 딥러닝 분야에서는 라벨링이나 실험 설정(Configuration) 값을 저장할 때 자주 접하게 됩니다.

{% highlight json %}
{
"id": 0,
"bbox": [0.5, 0.5, 0.2, 0.3],
"category": "person",
"is_crowd": false
}
{% endhighlight %}

앞서 언급한 COCO 포맷은 이러한 JSON의 특징을 활용해 하나의 파일에 수십만 개의 라벨 데이터를 체계적으로 적재합니다. 또한 실험 시 특정 하이퍼파라미터만 수정하고 싶을 때, 해당 키값만 변경하면 되므로 매우 직관적입니다.


**"YAML (YAML Ain't Markup Language)"**
YAML은 "마크업 언어라기보다 데이터를 더 잘 나타내자"는 목적에 집중한 포맷입니다. JSON과 마찬가지로 Key-Value 쌍을 사용하지만, 훨씬 인간 친화적입니다.

{% highlight yaml %}
model:
name: "yolov8"
epochs: 100
dataset:
path: "/data/custom"
batch_size: 16
{% endhighlight %}

**"JSON이 있는데 왜 YAML을 쓰나요?"**라는 의문이 들 수 있습니다. YAML은 들여쓰기, 주석(#), 하이픈(-) 등을 지원하여 훨씬 직관적입니다. 개발은 나만 알아보는 것이 아니라 타인과의 **'공유'**가 핵심이기에, 가독성이 좋은 YAML은 실험 환경 공유 시 최고의 선택지가 됩니다.
다음엔 실제로 YAML을 딥러닝 실험에서 어떻게 활용하는지, 유지보수를 어떻게 하는지 알아보도록 하겠습니다. 