# News Recommendation

뉴스 추천 시스템 관련 모델들을 일부 구현해보았습니다.

**Models in published papers**

| Model     | Full name                                                                 | Paper                                              |
| --------- | ------------------------------------------------------------------------- | -------------------------------------------------- |
| NRMS      | Neural News Recommendation with Multi-Head Self-Attention                 | https://www.aclweb.org/anthology/D19-1671/         |
| NAML      | Neural News Recommendation with Attentive Multi-View Learning             | https://arxiv.org/abs/1907.05576                   |

**Experimental models**

| Model | Description                                                                                        |
| ----- | -------------------------------------------------------------------------------------------------- |
| Exp1  | NRMS + (Sub)category + Ensemble + Positional embedding                                             |

## 학습하기

- 필수 패키지 설치
```bash
pip3 install -r requirements.txt
```
- Data 및 임베딩 다운로드
[MIND: MIcrosoft News Dataset](https://msnews.github.io/)
```bash
mkdir data && cd data
# Download GloVe pre-trained word embedding
wget https://nlp.stanford.edu/data/glove.840B.300d.zip
sudo apt install unzip
unzip glove.840B.300d.zip -d glove
rm glove.840B.300d.zip

# Download MIND dataset
# MIND dataset은 크기가 방대해 학습에 어려움이 있으니 small dataset을 사용하겠습니다.
wget https://mind201910small.blob.core.windows.net/release/MINDsmall_train.zip https://mind201910small.blob.core.windows.net/release/MINDsmall_dev.zip
unzip MINDsmall_train.zip -d train
unzip MINDsmall_dev.zip -d val 
# small data는 test 셋이 없어 validation 셋을 test data로 사용
cp -r val test
rm MINDsmall_*.zip

cd ..
python3 data_preprocess.py
```

Modify `config.py` to select target model. 

```bash
vim config.py
```

Run.

```bash
# Train and save checkpoint into `checkpoint/{model_name}/` 
python3 train.py
# Load latest checkpoint and evaluate on the test set
python3 evaluate.py
```
