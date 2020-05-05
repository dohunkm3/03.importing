- - -

# 판다스 입문 : 데이터 호출 및 저장

### Pandas Primer: Merging DataFrame - Accessing & Saving Text Files

* * *

**박 진 수** 교수  
Intelligent Data Semantics Lab  
Seoul National University

- - -

<h3>Table of Contents<span class="tocSkip"></span></h3>
<div class="toc"><ul class="toc-item"><li><span><a href="#실습-파일-내려받기" data-toc-modified-id="실습-파일-내려받기-1">실습 파일 내려받기</a></span></li><li><span><a href="#CSV와-텍스트-데이터" data-toc-modified-id="CSV와-텍스트-데이터-2">CSV와 텍스트 데이터</a></span></li><li><span><a href="#엑셀-데이터-불러오기" data-toc-modified-id="엑셀-데이터-불러오기-3">엑셀 데이터 불러오기</a></span><ul class="toc-item"><li><span><a href="#Lab:-엑셀-파일을-데이터프레임으로-불러오기" data-toc-modified-id="Lab:-엑셀-파일을-데이터프레임으로-불러오기-3.1">Lab: 엑셀 파일을 데이터프레임으로 불러오기</a></span></li></ul></li><li><span><a href="#HTML-파일-불러오기" data-toc-modified-id="HTML-파일-불러오기-4">HTML 파일 불러오기</a></span></li><li><span><a href="#JSON-파일-불러오기" data-toc-modified-id="JSON-파일-불러오기-5">JSON 파일 불러오기</a></span></li><li><span><a href="#클립보드-내용-불러오기" data-toc-modified-id="클립보드-내용-불러오기-6">클립보드 내용 불러오기</a></span></li><li><span><a href="#데이터-저장하기" data-toc-modified-id="데이터-저장하기-7">데이터 저장하기</a></span><ul class="toc-item"><li><span><a href="#Lab:-데이터프레임을-엑셀-파일로-저장하기" data-toc-modified-id="Lab:-데이터프레임을-엑셀-파일로-저장하기-7.1">Lab: 데이터프레임을 엑셀 파일로 저장하기</a></span></li></ul></li></ul></div>


```python
import pandas  # as pd
pandas.__version__
```

# 실습 파일 내려받기

데이터 파일을 내려받는다.


```python
# --- 만약 wget이 설치되어 있다면 아래 명령어로 모든 파일을 'data'라는 하위 폴더에 내려받는다.

# 하위 폴더 'data'가 없으면 새로 만든다.
import os
if not os.path.exists('data'):
    os.makedirs('data')  

!wget -O data/csv_data.csv -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=15bNIuuFsEAhAaL0EkVjm4ZW32MjjNjFe'
!wget -O data/csv_data_no_header.csv -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=1K8mCBeD-ytafeCDg3jMpOKuzlnJ_aBfd'
!wget -O data/csv_data_semicolon.csv -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=1EkvCWCrmgsKXsXppF_PcdzL1DGP7r2c5'
!wget -O data/excel_data.xlsx -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=1e1Jai4Gob62F9Ijut3AYxJrrzbyC7PTO'
!wget -O data/animals.xlsx -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=1HXMoFKGi_z8XLPWvJaKAnOsdYejSv5z4'
!wget -O data/NBA_2019_totals.html -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=1mB6jU4tP_clxt0DuyBMH5z68zRnGz6nA'
!wget -O data/bitcoin_price.json -q --show-progress --no-check-certificate 'https://docs.google.com/uc?export=download&id=10O0GyM3uyC9H8XBBVcQS_qyi9sc_jR07'
```

    data/csv_data.csv   100%[===================>]      63  --.-KB/s    in 0s      
    data/csv_data_no_he 100%[===================>]      50  --.-KB/s    in 0s      
    data/csv_data_semic 100%[===================>]      68  --.-KB/s    in 0s      
    data/excel_data.xls 100%[===================>]   8.52K  --.-KB/s    in 0s      
    data/animals.xlsx   100%[===================>]  17.46K  --.-KB/s    in 0.03s   
    data/NBA_2019_total 100%[===================>]   1.23M  4.21MB/s    in 0.3s    
    data/bitcoin_price. 100%[===================>]     511  --.-KB/s    in 0s      


**wget**을 설치하지 않았다면 아래 링크를 선택하여 내려받는다. 파일을 내려받은 후 파일 이름이 아래 이름과 일치하는지 꼭 확인하기 바란다.
- [csv_data.csv](https://docs.google.com/uc?export=download&id=15bNIuuFsEAhAaL0EkVjm4ZW32MjjNjFe) 
- [csv_data_no_header.csv](https://docs.google.com/uc?export=download&id=1K8mCBeD-ytafeCDg3jMpOKuzlnJ_aBfd)
- [csv_data_semicolon.csv](https://docs.google.com/uc?export=download&id=1EkvCWCrmgsKXsXppF_PcdzL1DGP7r2c5)
- [excel_data.xlsx](https://docs.google.com/uc?export=download&id=1e1Jai4Gob62F9Ijut3AYxJrrzbyC7PTO)
- [animals.xlsx](https://docs.google.com/uc?export=download&id=1HXMoFKGi_z8XLPWvJaKAnOsdYejSv5z4)
- [NBA_2019_totals.html](https://docs.google.com/uc?export=download&id=1mB6jU4tP_clxt0DuyBMH5z68zRnGz6nA)
- [bitcoin_price.json](https://docs.google.com/uc?export=download&id=10O0GyM3uyC9H8XBBVcQS_qyi9sc_jR07)

내려받은 모든 파일은 현재 작업 폴더의 하위 폴더인 'data'에 있다고 가정한다.

# CSV와 텍스트 데이터 

**CSV**(comma-separated values)란?
- 데이터의 각 열을 쉼표(**,**)로 구분하여 저장하는 텍스트 파일이다.
- 확장자는 **.csv**다.
- 각 열의 구분자(delimiter)로 쉼표(**,**)가 일반적이지만, 탭('**\t**'), 쌍반점('**;**') 등의 구분자도 자주 사용한다. 

판다스(Pandas)도 넘파이(NumPy)와 유사하게 CSV와 텍스트(text) 데이터를 불러올 수 있다.
- **read_csv()** 메소드로 CSV 파일의 데이터를 불러오면 자동으로 데이터프레임으로 저장한다.
- **read_table()** 메소드로 텍스트(text) 파일의 데이터를 불러오면 자동으로 데이터프레임으로 저장한다.

[pandas.read_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html#pandas.read_csv)
- Read a comma-separated values (csv) file into DataFrame.
- Also supports optionally iterating or breaking of the file into chunks.
- pandas.**read_csv**(*filepath_or_buffer: Union[str, pathlib.Path, IO[~AnyStr]], sep=',', delimiter=None, header='infer', names=None, index_col=None, usecols=None, squeeze=False, prefix=None, mangle_dupe_cols=True, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skipinitialspace=False, skiprows=None, skipfooter=0, nrows=None, na_values=None, keep_default_na=True, na_filter=True, verbose=False, skip_blank_lines=True, parse_dates=False, infer_datetime_format=False, keep_date_col=False, date_parser=None, dayfirst=False, cache_dates=True, iterator=False, chunksize=None, compression='infer', thousands=None, decimal=b'.', lineterminator=None, quotechar='"', quoting=0, doublequote=True, escapechar=None, comment=None, encoding=None, dialect=None, error_bad_lines=True, warn_bad_lines=True, delim_whitespace=False, low_memory=True, memory_map=False, float_precision=None*)

[pandas.read_table](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_table.html#pandas.read_table)
- Read general delimited file into DataFrame.
- Also supports optionally iterating or breaking of the file into chunks.
- pandas.**read_table**(*filepath_or_buffer: Union[str, pathlib.Path, IO[~AnyStr]], sep='t', delimiter=None, header='infer', names=None, index_col=None, usecols=None, squeeze=False, prefix=None, mangle_dupe_cols=True, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skipinitialspace=False, skiprows=None, skipfooter=0, nrows=None, na_values=None, keep_default_na=True, na_filter=True, verbose=False, skip_blank_lines=True, parse_dates=False, infer_datetime_format=False, keep_date_col=False, date_parser=None, dayfirst=False, cache_dates=True, iterator=False, chunksize=None, compression='infer', thousands=None, decimal=b'.', lineterminator=None, quotechar='"', quoting=0, doublequote=True, escapechar=None, comment=None, encoding=None, dialect=None, error_bad_lines=True, warn_bad_lines=True, delim_whitespace=False, low_memory=True, memory_map=False, float_precision=None*)


```python
%pycat data/csv_data.csv
```


    [0mID[0m[0;34m,[0m[0mLAST_NAME[0m[0;34m,[0m[0mAGE[0m[0;34m[0m
    [0;34m[0m[0;36m1[0m[0;34m,[0m[0mKIM[0m[0;34m,[0m[0;36m30[0m[0;34m[0m
    [0;34m[0m[0;36m2[0m[0;34m,[0m[0mCHOI[0m[0;34m,[0m[0;36m25[0m[0;34m[0m
    [0;34m[0m[0;36m3[0m[0;34m,[0m[0mLEE[0m[0;34m,[0m[0;36m41[0m[0;34m[0m
    [0;34m[0m[0;36m4[0m[0;34m,[0m[0mPARK[0m[0;34m,[0m[0;36m19[0m[0;34m[0m
    [0;34m[0m[0;36m5[0m[0;34m,[0m[0mLIM[0m[0;34m,[0m[0;36m36[0m[0;34m[0m[0;34m[0m[0m




```python
# CSV 파일('csv_data.csv')을 불러온다. 
# read_csv()의 기본 구분자는 콤마(',')이다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME  AGE
0   1       KIM   30
1   2      CHOI   25
2   3       LEE   41
3   4      PARK   19
4   5       LIM   36
</pre>


```python
# 특정 열만 (열 위치로) 선택하여 불러온다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
  LAST_NAME  AGE
0       KIM   30
1      CHOI   25
2       LEE   41
3      PARK   19
4       LIM   36
</pre>


```python
# 특정 열만 (열 이름으로) 선택하여 불러온다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME
0   1       KIM
1   2      CHOI
2   3       LEE
3   4      PARK
4   5       LIM
</pre>


```python
# read_table()을 사용하면 매개변수 sep에 구분자를 설정해야 한다.
# read_table()의 기본 구분자는 탭('\t')이다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME  AGE
0   1       KIM   30
1   2      CHOI   25
2   3       LEE   41
3   4      PARK   19
4   5       LIM   36
</pre>


```python
# read_table()로 특정 열만 (열 이름으로) 선택하여 불러온다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME
0   1       KIM
1   2      CHOI
2   3       LEE
3   4      PARK
4   5       LIM
</pre>


```python
# -- 열 이름이 없는 CSV 파일
%pycat data/csv_data_no_header.csv
```


    [0;36m1[0m[0;34m,[0m[0mKIM[0m[0;34m,[0m[0;36m30[0m[0;34m[0m
    [0;34m[0m[0;36m2[0m[0;34m,[0m[0mCHOI[0m[0;34m,[0m[0;36m25[0m[0;34m[0m
    [0;34m[0m[0;36m3[0m[0;34m,[0m[0mLEE[0m[0;34m,[0m[0;36m41[0m[0;34m[0m
    [0;34m[0m[0;36m4[0m[0;34m,[0m[0mPARK[0m[0;34m,[0m[0;36m19[0m[0;34m[0m
    [0;34m[0m[0;36m5[0m[0;34m,[0m[0mLIM[0m[0;34m,[0m[0;36m36[0m[0;34m[0m[0;34m[0m[0m




```python
# 열 이름이 없는 CSV 파일('csv_data_no_header.csv')을 불러온다. 
# 그런데 첫 번째 행이 열 이름으로 된다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   1   KIM  30
0  2  CHOI  25
1  3   LEE  41
2  4  PARK  19
3  5   LIM  36
</pre>


```python
# 따라서 열 이름이 없는 CSV 파일을 불러올 때 열 이름이 없다고 설정해야 한다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   0     1   2
0  1   KIM  30
1  2  CHOI  25
2  3   LEE  41
3  4  PARK  19
4  5   LIM  36
</pre>


```python
# -- 구분자가 쉼표','가 아닌 CSV 파일
%pycat data/csv_data_semicolon.csv
```


    [0mID[0m[0;34m;[0m[0mLAST_NAME[0m[0;34m;[0m[0mAGE[0m[0;34m[0m
    [0;34m[0m[0;36m1[0m[0;34m;[0m[0mKIM[0m[0;34m;[0m[0;36m30[0m[0;34m[0m
    [0;34m[0m[0;36m2[0m[0;34m;[0m[0mCHOI[0m[0;34m;[0m[0;36m25[0m[0;34m[0m
    [0;34m[0m[0;36m3[0m[0;34m;[0m[0mLEE[0m[0;34m;[0m[0;36m41[0m[0;34m[0m
    [0;34m[0m[0;36m4[0m[0;34m;[0m[0mPARK[0m[0;34m;[0m[0;36m19[0m[0;34m[0m
    [0;34m[0m[0;36m5[0m[0;34m;[0m[0mLIM[0m[0;34m;[0m[0;36m36[0m[0;34m[0m[0;34m[0m[0m




```python
# 구분자가 쉼표','가 아닌 CSV 파일('csv_data_semicolon.csv')을 
# 읽을 때는 매개변수 sep에 구분자를 설정해야 한다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME  AGE
0   1       KIM   30
1   2      CHOI   25
2   3       LEE   41
3   4      PARK   19
4   5       LIM   36
</pre>


```python
# read_table()을 사용해도 같은 결과를 가져온다.
# read_table()의 기본 구분자는 탭('\t')이다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME  AGE
0   1       KIM   30
1   2      CHOI   25
2   3       LEE   41
3   4      PARK   19
4   5       LIM   36
</pre>


```python
# 특정 열만 (열 이름으로) 선택하여 불러온다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
  LAST_NAME  AGE
0       KIM   30
1      CHOI   25
2       LEE   41
3      PARK   19
4       LIM   36
</pre>

# 엑셀 데이터 불러오기 

판다스(Pandas)에서는 엑셀(excel) 형태(.xlsx/.xls)의 데이터도 쉽게 불러올 수 있다.
- **read_excel()** 메소드를 통해 데이터를 불러오면 자동으로 데이터프레임으로 저장된다.
    + 매개변수 ***sheet_name***을 설정하지 않으면 기본값인 **0**으로 첫 번째 sheet를 가져온다.
    + ***sheet_name***으로 숫자가 올 수도 있고 sheet 이름이 올 수도 있다. **1**은 두 번째 sheet다.
    + ***sheet_name=None***은 모든 sheet를 가져온다.

[pandas.read_excel](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_excel.html#pandas.read_excel)
- Read an Excel file into a pandas DataFrame.
- Support both **xls** and **xlsx** file extensions from a local filesystem or URL. 
    - Support an option to read a single sheet or a list of sheets.
- pandas.**read_excel**(*io, sheet_name=0, header=0, names=None, index_col=None, usecols=None, squeeze=False, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skiprows=None, nrows=None, na_values=None, keep_default_na=True, verbose=False, parse_dates=False, date_parser=None, thousands=None, comment=None, skip_footer=0, skipfooter=0, convert_float=True, mangle_dupe_cols=True, \*\*kwds*)

엑셀 파일을 처리하려면 [xlrd](https://xlrd.readthedocs.io/en/latest/) 모듈을 설치해야 한다.


```python
# 엑셀 파일을 처리하려면 xlrd 모듈을 설치해야 한다.
!pip install --upgrade xlrd
```


```python
# 엑셀 파일('excel_data.xlsx')을 불러온다. 
# sheet_name을 설정하지 않으면 기본값인 0으로 첫 번째 sheet를 가져온다.
# sheet_name으로 숫자가 올 수도 있고 sheet 이름이 올 수도 있다.
# sheet_name=None은 모든 sheet를 가져온다.
df = __TODO__
print(df)
```

**실행 결과**
<pre>
   ID LAST_NAME  AGE
0   1       KIM   30
1   2      CHOI   25
2   3       LEE   41
3   4      PARK   19
4   5       LIM   36
</pre>

## Lab: 엑셀 파일을 데이터프레임으로 불러오기

---

- 하위 폴더 **data**에 있는 'animals.xlsx' 파일을 불러와 데이터프레임을 생성한 후 출력한다.
- 엑셀 파일의 첫 세 컬럼('name', 'hair', 'feathers')의 데이터만 포함하는 데이터프레임을 생성한 후 출력한다.

---

**답**


```python
# Your answer here
```

# HTML 파일 불러오기 

**HTML**(hypertext markup language)이란?
- 웹페이지 문서를 작성하는 언어다.
- 확장자는 **.html**, **.htm**이다.
- 홑화살괄호 (**<  >**)로 구분되는 태그들로 구성되어 있는 파일 형식이다.

판다스(Pandas)에서는 HTML 문서에 있는 표(table) 데이터를 쉽게 불러올 수 있다.
- **read_html()** 메소드는 HTML문서에서 표(<**table**> 태그)에 해당하는 부분만 자동으로 읽어온다.
    + pandas.**read_html**(*url*)
    + pandas.**read_html**(*filepath*)
    + **[주의]** : **read_html()** 메소드는 데이터프레임을 담은 **리스트**를 반환한다.    

[pandas.read_html](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_html.html)
- Read HTML tables into a list of DataFrame objects.
- pandas.**read_html**(*io, match='.+', flavor=None, header=None, index_col=None, skiprows=None, attrs=None, parse_dates=False, thousands=', ', encoding=None, decimal='.', converters=None, na_values=None, keep_default_na=True, displayed_only=True*)


```python
# 해당 url의 html 파일 중 태그가 <table>로 구성되어 있는 데이터를 가져온다.
# 이 때 read_html() 메소드는 데이터프레임을 담은 리스트를 반환한다.
url = 'https://www.basketball-reference.com/leagues/NBA_2019_totals.html'
list_of_dfs = __TODO__
df = __TODO__
print(df)
```

**실행 결과**
<pre>
      Rk        Player Pos Age   Tm   G  GS  ...  TRB  AST  STL BLK  TOV   PF   PTS
0      1  Álex Abrines  SG  25  OKC  31   2  ...   48   20   17   6   14   53   165
1      2    Quincy Acy  PF  28  PHO  10   0  ...   25    8    1   4    4   24    17
2      3  Jaylen Adams  PG  22  ATL  34   1  ...   60   65   14   5   28   45   108
3      4  Steven Adams   C  25  OKC  80  80  ...  760  124  117  76  135  204  1108
4      5   Bam Adebayo   C  21  MIA  82  28  ...  597  184   71  65  121  203   729
..   ...           ...  ..  ..  ...  ..  ..  ...  ...  ...  ...  ..  ...  ...   ...
729  528  Tyler Zeller   C  29  MEM   4   1  ...   18    3    1   3    4   16    46
730  529    Ante Žižić   C  22  CLE  59  25  ...  320   53   13  22   61  113   459
731  530   Ivica Zubac   C  21  TOT  59  37  ...  362   63   14  51   70  137   525
732  530   Ivica Zubac   C  21  LAL  33  12  ...  162   25    4  27   33   73   281
733  530   Ivica Zubac   C  21  LAC  26  25  ...  200   38   10  24   37   64   244

[734 rows x 30 columns]
</pre>


```python
# 파일로 저장된 html 문서는 일반 파일처럼 파일 경로를 통해 해당 페이지의 <table> 내용을 가져온다.
# 가져올 html 파일은 'NBA_2019_totals.html'
list_of_dfs = __TODO__
df = __TODO__
print(df)
```

**실행 결과**
<pre>
      Rk        Player Pos Age   Tm   G  GS  ...  TRB  AST  STL BLK  TOV   PF   PTS
0      1  Álex Abrines  SG  25  OKC  31   2  ...   48   20   17   6   14   53   165
1      2    Quincy Acy  PF  28  PHO  10   0  ...   25    8    1   4    4   24    17
2      3  Jaylen Adams  PG  22  ATL  34   1  ...   60   65   14   5   28   45   108
3      4  Steven Adams   C  25  OKC  80  80  ...  760  124  117  76  135  204  1108
4      5   Bam Adebayo   C  21  MIA  82  28  ...  597  184   71  65  121  203   729
..   ...           ...  ..  ..  ...  ..  ..  ...  ...  ...  ...  ..  ...  ...   ...
729  528  Tyler Zeller   C  29  MEM   4   1  ...   18    3    1   3    4   16    46
730  529    Ante Žižić   C  22  CLE  59  25  ...  320   53   13  22   61  113   459
731  530   Ivica Zubac   C  21  TOT  59  37  ...  362   63   14  51   70  137   525
732  530   Ivica Zubac   C  21  LAL  33  12  ...  162   25    4  27   33   73   281
733  530   Ivica Zubac   C  21  LAC  26  25  ...  200   38   10  24   37   64   244

[734 rows x 30 columns]
</pre>

# JSON 파일 불러오기 

**JSON**(**J**ava**S**cript **O**bject **N**otation)이란?
- Lightweight data-interchange format
    + 사람이 읽을 수 있고 기계가 처리할 수 있는 경량 데이터 교환 형식이다.
    + 파이썬의 딕셔너리처럼 키:매핑값 형식으로 내용을 저장한다.
- 확장자는 **.json**이다. 
- 프로그래밍 언어와 플랫폼에 독립적이라 많은 응용 프로그램에서 데이터 교환용으로 많이 사용한다.
    + 특히 웹에서 데이터를 주고 받을 때 자주 사용하는 파일 형식이다.
- 추가 정보 : http://json.org    

**json** 형식은 파이썬의 딕셔너리와 유사하다. 하지만 트리(tree) 구조로 이해를 하는 것이 좀더 직관적이다.
- <https://www.sitepoint.com/demos/online-json-tree-viewer/>를 이용하면
- JSON 파일을 트리구조로 시각화 할 수 있다.



판다스(Pandas)에서는 JSON 파일도 쉽게 불러올 수 있다.
- **read_json()** 메소드를 통해 데이터를 불러오면 자동으로 데이터프레임으로 저장된다.
    + pandas.**read_json**(*url*)
    + pandas.**read_json**(*filepath*)

[pandas.read_json](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_json.html)
- Convert a JSON string to pandas object.
- pandas.**read_json**(*path_or_buf=None, orient=None, typ='frame', dtype=None, convert_axes=None, convert_dates=True, keep_default_dates=True, numpy=False, precise_float=False, date_unit=None, encoding=None, lines=False, chunksize=None, compression='infer'*)


```python
# 해당 url의 json 파일을 가져온다.
url = 'https://api.coindesk.com/v1/bpi/currentprice/KRW.json' 
df = __TODO__
print(df)
```

**실행 결과**
<pre>
updated      Apr 4, 2020 05:37:00 UTC  ...                                                NaN
updatedISO  2020-04-04T05:37:00+00:00  ...                                                NaN
updateduk    Apr 4, 2020 at 06:37 BST  ...                                                NaN
USD                               NaN  ...  {'code': 'USD', 'rate': '6,753.6150', 'descrip...
KRW                               NaN  ...  {'code': 'KRW', 'rate': '8,352,905.1627', 'des...

[5 rows x 3 columns]
</pre>


```python
# 파일로 저장된 json 문서는 일반 파일처럼 파일 경로를 통해 json 파일을 가져온다.
# 가져올 json 파일은 'bitcoin_price.json'
df = __TODO__
print(df)
```

**실행 결과**
<pre>
updated      Apr 4, 2020 05:37:00 UTC  ...                                                NaN
updatedISO  2020-04-04T05:37:00+00:00  ...                                                NaN
updateduk    Apr 4, 2020 at 06:37 BST  ...                                                NaN
USD                               NaN  ...  {'code': 'USD', 'rate': '6,753.6150', 'descrip...
KRW                               NaN  ...  {'code': 'KRW', 'rate': '8,352,905.1627', 'des...

[5 rows x 3 columns]
</pre>

[pandas.json_normalize](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.json_normalize.html)
- Normalize semi-structured JSON data into a flat table.
- pandas.**json_normalize**(*data: Union[Dict, List[Dict]], record_path: Union[str, List, NoneType]=None, meta: Union[str, List[Union[str, List[str]]], NoneType]=None, meta_prefix: Union[str, NoneType]=None, record_prefix: Union[str, NoneType]=None, errors: Union[str, NoneType]='raise', sep: str='.', max_level: Union[int, NoneType]=None*) 


```python
# json_normalize() 함수를 이용하여 중첩 구조의 json 파일을 평평한 테이블(flat table) 형식으로 변환한다.
# 가져올 json 파일은 'bitcoin_price.json'
import json
file = open(__TODO__)  # 파일은 연다.
data = json.load(__TODO__) # 파일을 json으로 불러온다.
df = __TODO__  # 중첩 json 파일 구조를 단순한 테이블 형식으로 정규화한다.
print(df)
```

**실행 결과**
<pre>
                                          disclaimer  ... bpi.KRW.rate_float
0  This data was produced from the CoinDesk Bitco...  ...       8.189593e+06

[1 rows x 12 columns]
</pre>

# 클립보드 내용 불러오기 

[pandas.read_clipboard](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_clipboard.html)
- Read text from clipboard and pass to read_csv.
- pandas.**read_clipboard**(*sep='\s+', **kwargs*)
    + ***sep*** : *str, default ‘s+’*
        - A string or regex delimiter. The default of ‘s+’ denotes one or more whitespace characters.
    + *****kwargs*** : See **read_csv** for the full argument list.

# 데이터 저장하기

판다스(Pandas)를 활용하면 csv 혹은 엑셀(excel) 형태의 데이터로 저장하는 것도 용이하다.
- **to_csv()**와 **to_excel()** 메소드를 사용한다.

[pandas.DataFrame.to_csv](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_csv.html#pandas.DataFrame.to_csv)
- Write object to a comma-separated values (csv) file.
- DataFrame.**to_csv**(*self, path_or_buf=None, sep=', ', na_rep='', float_format=None, columns=None, header=True, index=True, index_label=None, mode='w', encoding=None, compression='infer', quoting=None, quotechar='"', line_terminator=None, chunksize=None, date_format=None, doublequote=True, escapechar=None, decimal='.'*)

[pandas.DataFrame.to_excel](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.to_excel.html#pandas.DataFrame.to_excel)
- Write object to an Excel sheet.
- To write a single object to an Excel .xlsx file it is only necessary to specify a target file name. To write to multiple sheets it is necessary to create an *ExcelWriter* object with a target file name, and specify a sheet in the file to write to.
- Multiple sheets may be written to by specifying unique *sheet_name*. With all data written to the file, it is necessary to save the changes. Note that creating an *ExcelWriter* object with a file name that already exists will result in the contents of the existing file being erased.
- DataFrame.**to_excel**(*self, excel_writer, sheet_name='Sheet1', na_rep='', float_format=None, columns=None, header=True, index=True, index_label=None, startrow=0, startcol=0, engine=None, merge_cells=True, encoding=None, inf_rep='inf', verbose=True, freeze_panes=None*)


```python
df = pandas.read_csv('data/csv_data.csv')
print(df)
```

       ID LAST_NAME  AGE
    0   1       KIM   30
    1   2      CHOI   25
    2   3       LEE   41
    3   4      PARK   19
    4   5       LIM   36



```python
# 앞서 데이터프레임으로 읽어 들인 df를 CSV 파일 형식으로 저장한다.
# 매개변수 sep를 설정하지 않으면 기본값인 쉼표를 구분자로 하여 파일을 저장한다.
__TODO__
```

**실행 결과** : 오류가 안 나면 결과를 출력하지 않는다.


```python
# 파일이 잘 저장되었는지 확인한다.
%pycat data/data.csv
```


    [0;34m,[0m[0mID[0m[0;34m,[0m[0mLAST_NAME[0m[0;34m,[0m[0mAGE[0m[0;34m[0m
    [0;34m[0m[0;36m0[0m[0;34m,[0m[0;36m1[0m[0;34m,[0m[0mKIM[0m[0;34m,[0m[0;36m30[0m[0;34m[0m
    [0;34m[0m[0;36m1[0m[0;34m,[0m[0;36m2[0m[0;34m,[0m[0mCHOI[0m[0;34m,[0m[0;36m25[0m[0;34m[0m
    [0;34m[0m[0;36m2[0m[0;34m,[0m[0;36m3[0m[0;34m,[0m[0mLEE[0m[0;34m,[0m[0;36m41[0m[0;34m[0m
    [0;34m[0m[0;36m3[0m[0;34m,[0m[0;36m4[0m[0;34m,[0m[0mPARK[0m[0;34m,[0m[0;36m19[0m[0;34m[0m
    [0;34m[0m[0;36m4[0m[0;34m,[0m[0;36m5[0m[0;34m,[0m[0mLIM[0m[0;34m,[0m[0;36m36[0m[0;34m[0m[0;34m[0m[0m



엑셀 파일을 읽고 쓰려면 [openpyxl](https://openpyxl.readthedocs.io/en/stable/) 모듈을 설치해야 한다.


```python
# 엑셀 파일을 읽고 쓰려면 openpyxl 모듈을 설치해야 한다.
!pip install --upgrade openpyxl
```


```python
# 앞서 데이터프레임으로 읽어 들인 df를 엑셀 파일 형식으로 저장한다.
# 매개변수 sheet_name을 설정하면 sheet의 이름을 지정하고 저장할 수 있다.
__TODO__
```

**실행 결과** : 파일을 성공적으로 저장하면(즉, 오류가 안 나면) 결과는 출력하지 않는다.

## Lab: 데이터프레임을 엑셀 파일로 저장하기

---

- 앞서 < Lab: 엑셀 파일을 데이터프레임으로 불러오기 >에서 만든 데이터프레임의 데이터를 하위 폴더 **data**에 엑셀 파일로 저장한다.
- 저장할 파일 이름은 'animals_sub.xlsx'로 한다.

--- 

**답**


```python
# Your answer here
```

- - -

# THE END
