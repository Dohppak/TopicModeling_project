# Interview data analysis for UX  ver 1.0

Interview data analysis for UX
Interview data from 

## Process

1. 데이터 전처리 과정
- train_data : 인터뷰 text 데이터 불러오기
- train_docs : 형태소 분석을 통한 POS 태깅
- remove_item : Conjunction,Deteriner,Exclamation,Josa,Punctuation,Suffix
- trained_docs_list : 불용어 제거한 데이터 셋
- text : 토크나이즈 진행
  
2. 데이터 분석 과정
- doc2vec 에서 요구하는 전처리를 한번 더해준다
- 사전구축하고, vector들을 트레이닝시킨다.
- Topic Modeling : 어떤 문서에서 자주 나타는 단어를 통해, 주제를 찾아주는 확률적인 모델을 디자인합니다.유명한 것으로 LDA, LSI, HDP가 있습니다.
- Word Embedding : 문장속의 단어간의 관계를 비지도 학습 방식으로 분석하여 만들어지는 수십~ 수백차원의 벡터로서 특징(Feature)화 되는 단어들을 만들어 냅니다. 단어가 가지고있는 벡터간의 연산을 통해 다른 단어와의 관계를 만들어내게 됩니다
- Doc2Vec(dbow+w,d300,n10,hs,w8,mc5,s0.001,t4) : DBOW 방식,Window 8, vector : 300, learning-rate : 0.025, min_count : 5, Multi CPU, Hierachical softmax, megative sampling)


## Data description

- 16 Documents (Sample number!)
- 1732 Sentences (unit!)
- Each file is consisted of two columns: `id`, `document`
    - `id`: Interviewer and Interviewee
    - `document`: Contents

## Characteristics
- Interview data : Question and answer format, Question's sementic meaning is same.
- Semi-structured : Open answer, so unexpected topic can exist.
- Doc-Sentence-Word : 3 depth format


## Quick peek
      $Interview example
        ID	TEXT
      0	DSJY	자 저희는 유니스트 소속 대학원 수업 CONTEXTUAL DESGIN 을 수강하고 ...
      1	P2	네
      2	DSJY	보나는 어떤 집단인지 궁금합니다
      3	P2	우리는 습관에 대해서 항상하고 사람들이 움직이는 방법에 대해서 건강한 습관을 가지고...
      4	DSJY	굉장히 좋은 취지인것 같습니다
      5	P2	그렇죠? 우리팀에서 일할래?
      6	DSJY	돈주면..., 보나의 규모가 어느정도인가요?
      7	P2	규모라는게 너무 작아서 규모라고 할 정도가 아니고 정말 작아서 그냥 1인기업, 스타...
      8	DSJY	업무환경에 대해서 말씀해 주실수 있나요? 오피스의 컴퓨터라던지?
      9	P	2오피스에 컴퓨터 한대 그리고 회의가능하게 화이트보드가 있고, 업무환경의 소프트웨어...
      $
## Visualization
- using pyLDAvis.gensim

## Using

> from importlib import reload
<br/>
> import sys
<br/>
> import gensim
<br/>
> from gensim.models import doc2vec
<br/>
> from gensim.models.doc2vec import TaggedDocument
<br/>
> from collections import namedtuple
<br/>
> import pandas as pd
<br/>
> import smart_open
<br/>
> import random
<br/>
> import chardet
