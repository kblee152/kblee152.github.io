

#### 데이터 준비 및 병합

##### 로컬 CSV 파일은 Colab에 업로드 및 병합하기
```python
import pandas as pd
import glob
import os.path

# Colab에 local 파일 업로드
from google.colab import files
uploaded = files.upload()

for fn in uploaded.keys():
  print('User uploaded file "{name}" with length {length} bytes'.format(name = fn, length = len(uploaded[fn])))

# 디렉토리 내 위치한 파일을 병합하고 저장
input_file = r'C:/Users/kblee/documents/citibike-dataset' # csv파일들이 있는 디렉토리 위치
output_file = r'C:/Users/kblee/documents/citibike-dataset/result.csv' # 병합하고 저장하려는 파일명

allFile_list = glob.glob(os.path.join(input_file, 'JC-20*')) # glob함수로 sales_로 시작하는 파일e들을 모은다
print(allFile_list)

allData = [] # 읽어 들인 csv파일 내용을 저장할 빈 리스트를 하나 만든다
for file in allFile_list:
    df = pd.read_csv(file) # for구문으로 csv파일들을 읽어 들인다
    allData.append(df) # 빈 리스트에 읽어 들인 내용을 추가한다

dataCombine = pd.concat(allData, axis=0, ignore_index=True) # concat함수를 이용해서 리스트의 내용을 병합
dataCombine.to_csv(output_file, index=False) # to_csv함수로 저장한다. 인데스를 빼려면 False로 설정
```

##### Google bigquery를 Colab에 연동하기
```python
query = """
 SELECT 
  DATETIME(start_time) AS date,
  COUNT(trip_id) AS count
FROM `bigquery-public-data.austin_bikeshare.bikeshare_trips`
GROUP BY date
ORDER BY date
  """

df = pd.read_gbq(query = query, project_id='cb-259807', dialect='standard')
```
