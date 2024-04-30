---
title: 
---

# 8장. 챗봇 엔진 만들기
## 8.2. 챗봇 엔진 구조

* 챗봇 엔진의 핵심기능
① 질문 의도 분류 : 화자의 질문의도 파악. 해당 질문을 의도 분류 모델을 이용해 의도 클래스를 예측
② 개체명 인식 : 화자의 질문에서 단어 토큰별 개체명 인식. 단어 토큰에 맞는 개체명을 예측하는 문제
③ 핵심 키워드 추출 : 화자의 질문의미에서 핵심이 될만한 단어 토큰을 추출. 형태소 분석기를 이용해 핵심 키워드가 되는 명사나 동사를 추출
④ 답변 검색 : 해당 질문의 의도, 개체명, 핵심 키워드 등을 기반으로 답변을 학습 DB에서 검색
⑤ 소켓 서버 : 다양한 종류의 챗봇 클라이언트(카카오톡, 네이버톡톡)의 챗봇 클라이언트에서 요청하는 질문을 처리하기 위해 소켓 서버 프로그램 역할을 한다. 


* 챗봇 엔진 처리 과정
① 전처리
② 의도분석
③ 개체명 인식
④ 답변 검색
⑤ 답변 출력

* 챗봇 엔진에는 자연어 처리를 위해 2가지 딥러닝 모델(의도분석, 개체명인식)을 사용


## 8.3. 전처리 과정
형태소 분석기로 토크나이징 작업
문장 해석에 의미있는 정보만 남기고 나머지 불용어들은 제거

```
from konlpy.tag import Komoran
import pickle
import jpype


class Preprocess:
    def __init__(self, word2index_dic='', userdic=None):
        # 단어 인덱스 사전 불러오기
        if(word2index_dic != ''):
            f = open(word2index_dic, "rb")
            self.word_index = pickle.load(f)
            f.close()
        else:
            self.word_index = None

        # 형태소 분석기 초기화
        self.komoran = Komoran(userdic=userdic)

        # 제외할 품사
        # 참조 : https://docs.komoran.kr/firststep/postypes.html
        # 관계언 제거, 기호 제거
        # 어미 제거
        # 접미사 제거
        self.exclusion_tags = [
            'JKS', 'JKC', 'JKG', 'JKO', 'JKB', 'JKV', 'JKQ',
            'JX', 'JC',
            'SF', 'SP', 'SS', 'SE', 'SO',
            'EP', 'EF', 'EC', 'ETN', 'ETM',
            'XSN', 'XSV', 'XSA'
        ]

    # 형태소 분석기 POS 태거
    def pos(self, sentence):
        jpype.attachThreadToJVM()
        return self.komoran.pos(sentence)

    # 불용어 제거 후, 필요한 품사 정보만 가져오기
    def get_keywords(self, pos, without_tag=False):
        f = lambda x: x in self.exclusion_tags
        word_list = []
        for p in pos:
            if f(p[1]) is False:
                word_list.append(p if without_tag is False else p[0])
        return word_list

    # 키워드를 단어 인덱스 시퀀스로 변환
    def get_wordidx_sequence(self, keywords):
        if self.word_index is None:
            return []

        w2i = []
        for word in keywords:
            try:
                w2i.append(self.word_index[word])
            except KeyError:
                # 해당 단어가 사전에 없는 경우, OOV 처리
                w2i.append(self.word_index['OOV'])
        return w2i

```


















---