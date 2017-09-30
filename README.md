# mecab-java-msvc

[![Build status](https://ci.appveyor.com/api/projects/status/bxtc772o72obpkvb/branch/master?svg=true)](https://ci.appveyor.com/project/Pusnow/mecab-java-msvc/branch/master)

mecab-java-msvc는 mecab-ko-msvc에서 사용할 수 있는 mecab-java을 빌드하는 프로젝트입니다.

## 설치

* [mecab-ko-msvc](https://github.com/Pusnow/mecab-ko-msvc/)를 설치하지 않았으면 설치해야 합니다.
* [mecab-ko-dic-msvc](https://github.com/Pusnow/mecab-ko-dic-msvc/)를 설치하지 않았으면 설치해야 합니다.
* `C:\mecab\`을 PATH 환경변수에 추가합니다.
* 실행 환경에 맞는 [최신버전](https://github.com/Pusnow/mecab-java-msvc/releases/latest)을 다운로드합니다. JDK 1.8을 지원합니다.

## 사용 정보
* `org` 폴더와 `MeCab.dll`이 있는 경로에서 Java 파일을 편집합니다.
* 첨부한 `test.java`는 UTF-8로 인코딩 되어 있습니다. `javac -encoding UTF-8 test.java` 처럼 인코딩을 지정해 주어야 합니다.
* `java test` 로 테스트 파일을 실행할 수 있습니다.


## 빌드 정보

* mecab-java-msvc 는 [Appveyor](https://www.appveyor.com)를 이용합니다.
* 빌드 과정은 [Appveyor 페이지](https://ci.appveyor.com/project/Pusnow/mecab-java-msvc) 에 기록되어 있습니다.
* 개인적으로 빌드를 하고 싶으신 분은 [appveyor.yml](https://github.com/Pusnow/mecab-java-msvc/blob/master/appveyor.yml) 을 참고하시기 바랍니다.

## Elastic Search 연동

mecab-java-msvc는 Windows 환경에서 Elastic Search와 연동하여 사용할 수 있습니다. Windows 10 Ent. 64bit, JDK 1.8, Elastic Search 5.5.0 에서 테스트 완료했습니다.

### 세부 절차

1. mecab-ko-msvc을 `C:\mecab` 에 설치
2. mecab-ko-dic-msvc을 `C:\mecab` 에 설치
3. mecab-java-msvc에서 MeCab.dll을 `C:\mecab` 으로 복사
4. `C:\mecab` 을 환경변수 PATH에 추가
5. ElasticSearch 5.5.0 MSI 설치
6. 5.5.0 버전 플러그인 설치 
    1. 관리자의 권한으로 CMD 실행
    2. 다음 명령어를 실행하여 플러그인 설치
    3. `"C:\Program Files\Elastic\Elasticsearch\bin\elasticsearch-plugin.bat" install https://bitbucket.org/eunjeon/mecab-ko-lucene-analyzer/issues/attachments/9/eunjeon/mecab-ko-lucene-analyzer/1500357175.91/9/elasticsearch-analysis-mecab-ko-5.5.0.0.zip`
  4. ElasticSearch 재시작
  
  
### 테스트 (POSTMAN 사용)
1. 혹시 있을 eunjeon 제거 `DELETE http://localhost:9200/eunjeon`
2. 인데스 추가 리눅스 버전과 다르게 mecab_args로 사전 경로를 지정해 주어야 합니다. `PUT http://localhost:9200/eunjeon`
```
BODY(JSON):
    {
        "settings": {
            "index": {
            "analysis": {
                "analyzer": {
                "korean_index": {
                    "type": "custom",
                    "tokenizer": "mecab_ko_standard_tokenizer"
                },
                "korean_query": {
                    "type": "custom",
                    "tokenizer": "korean_query_tokenizer"
                }
                },
                "tokenizer": {
                "mecab_ko_standard_tokenizer": {
                    "type": "mecab_ko_standard_tokenizer",
                    "mecab_args": "-d C:/mecab/mecab-ko-dic"
                },
                "korean_query_tokenizer": {
                    "type": "mecab_ko_standard_tokenizer",
                    "compound_noun_min_length": 100,
                    "mecab_args": "-d C:/mecab/mecab-ko-dic"
                }
                }
            }
            }
        }
    }
```
3. 테스트 `POST http://localhost:9200/eunjeon/_analyze?analyzer=korean_query`
```
  BODY(text) : 은전한닢 프로젝트
```
4. 결과
```
{
    "tokens": [
        {
            "token": "은전",
            "start_offset": 0,
            "end_offset": 2,
            "type": "NNG",
            "position": 0
        },
        {
            "token": "한",
            "start_offset": 2,
            "end_offset": 3,
            "type": "NR",
            "position": 1
        },
        {
            "token": "닢",
            "start_offset": 3,
            "end_offset": 4,
            "type": "NNG",
            "position": 2
        },
        {
            "token": "프로젝트",
            "start_offset": 5,
            "end_offset": 9,
            "type": "NNG",
            "position": 3
        }
    ]
}
```



## 관련 프로젝트

* [Mecab-Ko-MSVC](https://github.com/Pusnow/mecab-ko-msvc)
* [Mecab-Ko-Dic-MSVC](https://github.com/Pusnow/mecab-ko-dic-msvc)
* [Mecab-Python-MSVC](https://github.com/Pusnow/mecab-python-msvc)


# mecab-java

[mecab-java](https://code.google.com/p/mecab/downloads/detail?name=mecab-java-0.996.tar.gz&can=2&q=) 의 tagger와 lexicon의 메모리 누수가 해결된 버전

MeCab java module

$Id: README,v 1.2 2005/12/25 16:55:43 taku-ku Exp $;

1. Build UTF-8 dictionary

2. How to use?

  See test.java as sample program.

  % java -classpath MeCab.jar test -d ../dic
