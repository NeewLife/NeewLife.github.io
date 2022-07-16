---
title: "PyCaret(함수자동생성기 세팅)"
output:
  html_document:
    keep_md: true
disqusIdentifier: fdsF34ff34
categories: Python
clearReading: true
thumbnailImage: pycaret.png
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
date: '2022-07-05 16:50:55'
---

- 언젠가는 쓸 수 있겠지? ㅎㅎ
<!-- excerpt -->


- PyCaret 설치
- https://github.com/pycaret/pycaret  에서 requirement.txt에 있는 목록 다 버전 맞춰서 깐다.


```python
!pip uninstall sklearn -y
!pip install --upgrade sklearn
!pip install scikit-learn==0.23.2 --user
!pip install pycaret
!pip install markupsafe==2.0.1
# 밑에 "RESTART RUMTIME" 을 클릭한다. (파란글씨 X)
```

- PyCaret을 구글 코랩에서 활성화


```python
from pycaret.utils import enable_colab
enable_colab()
```

    Colab mode enabled.
    

### 데이터 불러오기


```python
from pycaret.datasets import get_data
dataset = get_data('credit')
# credit 데이터 = 신용카드 연체 데이터, PyCaret 의 샘플 데이터이다.
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>





  <div id="df-c4307632-6e01-480c-9107-02c1c7afdd50">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>LIMIT_BAL</th>
      <th>SEX</th>
      <th>EDUCATION</th>
      <th>MARRIAGE</th>
      <th>AGE</th>
      <th>PAY_1</th>
      <th>PAY_2</th>
      <th>PAY_3</th>
      <th>PAY_4</th>
      <th>PAY_5</th>
      <th>...</th>
      <th>BILL_AMT4</th>
      <th>BILL_AMT5</th>
      <th>BILL_AMT6</th>
      <th>PAY_AMT1</th>
      <th>PAY_AMT2</th>
      <th>PAY_AMT3</th>
      <th>PAY_AMT4</th>
      <th>PAY_AMT5</th>
      <th>PAY_AMT6</th>
      <th>default</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20000</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>24</td>
      <td>2</td>
      <td>2</td>
      <td>-1</td>
      <td>-1</td>
      <td>-2</td>
      <td>...</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>689.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>90000</td>
      <td>2</td>
      <td>2</td>
      <td>2</td>
      <td>34</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>14331.0</td>
      <td>14948.0</td>
      <td>15549.0</td>
      <td>1518.0</td>
      <td>1500.0</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>5000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>50000</td>
      <td>2</td>
      <td>2</td>
      <td>1</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>28314.0</td>
      <td>28959.0</td>
      <td>29547.0</td>
      <td>2000.0</td>
      <td>2019.0</td>
      <td>1200.0</td>
      <td>1100.0</td>
      <td>1069.0</td>
      <td>1000.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>50000</td>
      <td>1</td>
      <td>2</td>
      <td>1</td>
      <td>57</td>
      <td>-1</td>
      <td>0</td>
      <td>-1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>20940.0</td>
      <td>19146.0</td>
      <td>19131.0</td>
      <td>2000.0</td>
      <td>36681.0</td>
      <td>10000.0</td>
      <td>9000.0</td>
      <td>689.0</td>
      <td>679.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>50000</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>37</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>19394.0</td>
      <td>19619.0</td>
      <td>20024.0</td>
      <td>2500.0</td>
      <td>1815.0</td>
      <td>657.0</td>
      <td>1000.0</td>
      <td>1000.0</td>
      <td>800.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-c4307632-6e01-480c-9107-02c1c7afdd50')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-c4307632-6e01-480c-9107-02c1c7afdd50 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-c4307632-6e01-480c-9107-02c1c7afdd50');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




```python
dataset.info()
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>



    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 24000 entries, 0 to 23999
    Data columns (total 24 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   LIMIT_BAL  24000 non-null  int64  
     1   SEX        24000 non-null  int64  
     2   EDUCATION  24000 non-null  int64  
     3   MARRIAGE   24000 non-null  int64  
     4   AGE        24000 non-null  int64  
     5   PAY_1      24000 non-null  int64  
     6   PAY_2      24000 non-null  int64  
     7   PAY_3      24000 non-null  int64  
     8   PAY_4      24000 non-null  int64  
     9   PAY_5      24000 non-null  int64  
     10  PAY_6      24000 non-null  int64  
     11  BILL_AMT1  24000 non-null  float64
     12  BILL_AMT2  24000 non-null  float64
     13  BILL_AMT3  24000 non-null  float64
     14  BILL_AMT4  24000 non-null  float64
     15  BILL_AMT5  24000 non-null  float64
     16  BILL_AMT6  24000 non-null  float64
     17  PAY_AMT1   24000 non-null  float64
     18  PAY_AMT2   24000 non-null  float64
     19  PAY_AMT3   24000 non-null  float64
     20  PAY_AMT4   24000 non-null  float64
     21  PAY_AMT5   24000 non-null  float64
     22  PAY_AMT6   24000 non-null  float64
     23  default    24000 non-null  int64  
    dtypes: float64(12), int64(12)
    memory usage: 4.4 MB
    


```python
data = dataset.sample(frac=0.95, random_state=786)
data_unseen = dataset.drop(data.index)
data.reset_index(inplace=True, drop=True)
data_unseen.reset_index(inplace=True, drop=True)
print('Data for Modeling: ' + str(data.shape))
print('Unseen Data For Predictions: ' + str(data_unseen.shape))
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>



    Data for Modeling: (22800, 24)
    Unseen Data For Predictions: (1200, 24)
    

- setup


```python
import jinja2
from pycaret.classification import *
exp_clf101 = setup(data = data, target = 'default', session_id=123)
# 빈 칸이 뜨면 엔터 치기
```



  <div id="df-02f377d0-f141-4491-8122-89a5f7a25949">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Description</th>
      <th>Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>session_id</td>
      <td>123</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Target</td>
      <td>default</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Target Type</td>
      <td>Binary</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Label Encoded</td>
      <td>None</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Original Data</td>
      <td>(22800, 24)</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Missing Values</td>
      <td>False</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Numeric Features</td>
      <td>14</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Categorical Features</td>
      <td>9</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Ordinal Features</td>
      <td>False</td>
    </tr>
    <tr>
      <th>9</th>
      <td>High Cardinality Features</td>
      <td>False</td>
    </tr>
    <tr>
      <th>10</th>
      <td>High Cardinality Method</td>
      <td>None</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Transformed Train Set</td>
      <td>(15959, 88)</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Transformed Test Set</td>
      <td>(6841, 88)</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Shuffle Train-Test</td>
      <td>True</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Stratify Train-Test</td>
      <td>False</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Fold Generator</td>
      <td>StratifiedKFold</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Fold Number</td>
      <td>10</td>
    </tr>
    <tr>
      <th>17</th>
      <td>CPU Jobs</td>
      <td>-1</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Use GPU</td>
      <td>False</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Log Experiment</td>
      <td>False</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Experiment Name</td>
      <td>clf-default-name</td>
    </tr>
    <tr>
      <th>21</th>
      <td>USI</td>
      <td>a6b7</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Imputation Type</td>
      <td>simple</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Iterative Imputation Iteration</td>
      <td>None</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Numeric Imputer</td>
      <td>mean</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Iterative Imputation Numeric Model</td>
      <td>None</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Categorical Imputer</td>
      <td>constant</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Iterative Imputation Categorical Model</td>
      <td>None</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Unknown Categoricals Handling</td>
      <td>least_frequent</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Normalize</td>
      <td>False</td>
    </tr>
    <tr>
      <th>30</th>
      <td>Normalize Method</td>
      <td>None</td>
    </tr>
    <tr>
      <th>31</th>
      <td>Transformation</td>
      <td>False</td>
    </tr>
    <tr>
      <th>32</th>
      <td>Transformation Method</td>
      <td>None</td>
    </tr>
    <tr>
      <th>33</th>
      <td>PCA</td>
      <td>False</td>
    </tr>
    <tr>
      <th>34</th>
      <td>PCA Method</td>
      <td>None</td>
    </tr>
    <tr>
      <th>35</th>
      <td>PCA Components</td>
      <td>None</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Ignore Low Variance</td>
      <td>False</td>
    </tr>
    <tr>
      <th>37</th>
      <td>Combine Rare Levels</td>
      <td>False</td>
    </tr>
    <tr>
      <th>38</th>
      <td>Rare Level Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>39</th>
      <td>Numeric Binning</td>
      <td>False</td>
    </tr>
    <tr>
      <th>40</th>
      <td>Remove Outliers</td>
      <td>False</td>
    </tr>
    <tr>
      <th>41</th>
      <td>Outliers Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>42</th>
      <td>Remove Multicollinearity</td>
      <td>False</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Multicollinearity Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>44</th>
      <td>Remove Perfect Collinearity</td>
      <td>True</td>
    </tr>
    <tr>
      <th>45</th>
      <td>Clustering</td>
      <td>False</td>
    </tr>
    <tr>
      <th>46</th>
      <td>Clustering Iteration</td>
      <td>None</td>
    </tr>
    <tr>
      <th>47</th>
      <td>Polynomial Features</td>
      <td>False</td>
    </tr>
    <tr>
      <th>48</th>
      <td>Polynomial Degree</td>
      <td>None</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Trignometry Features</td>
      <td>False</td>
    </tr>
    <tr>
      <th>50</th>
      <td>Polynomial Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>51</th>
      <td>Group Features</td>
      <td>False</td>
    </tr>
    <tr>
      <th>52</th>
      <td>Feature Selection</td>
      <td>False</td>
    </tr>
    <tr>
      <th>53</th>
      <td>Feature Selection Method</td>
      <td>classic</td>
    </tr>
    <tr>
      <th>54</th>
      <td>Features Selection Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>55</th>
      <td>Feature Interaction</td>
      <td>False</td>
    </tr>
    <tr>
      <th>56</th>
      <td>Feature Ratio</td>
      <td>False</td>
    </tr>
    <tr>
      <th>57</th>
      <td>Interaction Threshold</td>
      <td>None</td>
    </tr>
    <tr>
      <th>58</th>
      <td>Fix Imbalance</td>
      <td>False</td>
    </tr>
    <tr>
      <th>59</th>
      <td>Fix Imbalance Method</td>
      <td>SMOTE</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-02f377d0-f141-4491-8122-89a5f7a25949')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>



## 모델링


```python
best_model = compare_models()
```



  <div id="df-1f936788-ded9-461f-8219-3f16656853b9">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Model</th>
      <th>Accuracy</th>
      <th>AUC</th>
      <th>Recall</th>
      <th>Prec.</th>
      <th>F1</th>
      <th>Kappa</th>
      <th>MCC</th>
      <th>TT (Sec)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>ridge</th>
      <td>Ridge Classifier</td>
      <td>0.8254</td>
      <td>0.0000</td>
      <td>0.3637</td>
      <td>0.6913</td>
      <td>0.4764</td>
      <td>0.3836</td>
      <td>0.4122</td>
      <td>0.038</td>
    </tr>
    <tr>
      <th>lda</th>
      <td>Linear Discriminant Analysis</td>
      <td>0.8247</td>
      <td>0.7634</td>
      <td>0.3755</td>
      <td>0.6794</td>
      <td>0.4835</td>
      <td>0.3884</td>
      <td>0.4132</td>
      <td>0.300</td>
    </tr>
    <tr>
      <th>gbc</th>
      <td>Gradient Boosting Classifier</td>
      <td>0.8226</td>
      <td>0.7789</td>
      <td>0.3551</td>
      <td>0.6806</td>
      <td>0.4664</td>
      <td>0.3725</td>
      <td>0.4010</td>
      <td>5.707</td>
    </tr>
    <tr>
      <th>ada</th>
      <td>Ada Boost Classifier</td>
      <td>0.8221</td>
      <td>0.7697</td>
      <td>0.3505</td>
      <td>0.6811</td>
      <td>0.4626</td>
      <td>0.3690</td>
      <td>0.3983</td>
      <td>1.312</td>
    </tr>
    <tr>
      <th>lightgbm</th>
      <td>Light Gradient Boosting Machine</td>
      <td>0.8210</td>
      <td>0.7750</td>
      <td>0.3609</td>
      <td>0.6679</td>
      <td>0.4683</td>
      <td>0.3721</td>
      <td>0.3977</td>
      <td>0.420</td>
    </tr>
    <tr>
      <th>rf</th>
      <td>Random Forest Classifier</td>
      <td>0.8199</td>
      <td>0.7598</td>
      <td>0.3663</td>
      <td>0.6601</td>
      <td>0.4707</td>
      <td>0.3727</td>
      <td>0.3965</td>
      <td>3.079</td>
    </tr>
    <tr>
      <th>et</th>
      <td>Extra Trees Classifier</td>
      <td>0.8092</td>
      <td>0.7377</td>
      <td>0.3677</td>
      <td>0.6047</td>
      <td>0.4571</td>
      <td>0.3497</td>
      <td>0.3657</td>
      <td>2.547</td>
    </tr>
    <tr>
      <th>lr</th>
      <td>Logistic Regression</td>
      <td>0.7814</td>
      <td>0.6410</td>
      <td>0.0003</td>
      <td>0.1000</td>
      <td>0.0006</td>
      <td>0.0003</td>
      <td>0.0034</td>
      <td>1.005</td>
    </tr>
    <tr>
      <th>dummy</th>
      <td>Dummy Classifier</td>
      <td>0.7814</td>
      <td>0.5000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.0000</td>
      <td>0.029</td>
    </tr>
    <tr>
      <th>knn</th>
      <td>K Neighbors Classifier</td>
      <td>0.7547</td>
      <td>0.5939</td>
      <td>0.1763</td>
      <td>0.3719</td>
      <td>0.2388</td>
      <td>0.1145</td>
      <td>0.1259</td>
      <td>0.943</td>
    </tr>
    <tr>
      <th>dt</th>
      <td>Decision Tree Classifier</td>
      <td>0.7293</td>
      <td>0.6147</td>
      <td>0.4104</td>
      <td>0.3878</td>
      <td>0.3986</td>
      <td>0.2242</td>
      <td>0.2245</td>
      <td>0.378</td>
    </tr>
    <tr>
      <th>svm</th>
      <td>SVM - Linear Kernel</td>
      <td>0.7277</td>
      <td>0.0000</td>
      <td>0.1017</td>
      <td>0.1671</td>
      <td>0.0984</td>
      <td>0.0067</td>
      <td>0.0075</td>
      <td>0.498</td>
    </tr>
    <tr>
      <th>qda</th>
      <td>Quadratic Discriminant Analysis</td>
      <td>0.5098</td>
      <td>0.5473</td>
      <td>0.6141</td>
      <td>0.2472</td>
      <td>0.3488</td>
      <td>0.0600</td>
      <td>0.0805</td>
      <td>0.154</td>
    </tr>
    <tr>
      <th>nb</th>
      <td>Naive Bayes</td>
      <td>0.3760</td>
      <td>0.6442</td>
      <td>0.8845</td>
      <td>0.2441</td>
      <td>0.3826</td>
      <td>0.0608</td>
      <td>0.1207</td>
      <td>0.047</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-1f936788-ded9-461f-8219-3f16656853b9')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-1f936788-ded9-461f-8219-3f16656853b9 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-1f936788-ded9-461f-8219-3f16656853b9');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>



- 여기서 가장 좋은 모델을 뽑기


```python
print(best_model)
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>



    RidgeClassifier(alpha=1.0, class_weight=None, copy_X=True, fit_intercept=True,
                    max_iter=None, normalize=False, random_state=123, solver='auto',
                    tol=0.001)
    

- 모델 생성


```python
knn_model = create_model('knn')
# create_model('모델ID')
```



  <div id="df-dcfbc557-8ff3-4ddc-b12d-ac11d9486b3f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Accuracy</th>
      <th>AUC</th>
      <th>Recall</th>
      <th>Prec.</th>
      <th>F1</th>
      <th>Kappa</th>
      <th>MCC</th>
    </tr>
    <tr>
      <th>Fold</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.7469</td>
      <td>0.6020</td>
      <td>0.1920</td>
      <td>0.3545</td>
      <td>0.2491</td>
      <td>0.1128</td>
      <td>0.1204</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.7550</td>
      <td>0.5894</td>
      <td>0.2092</td>
      <td>0.3883</td>
      <td>0.2719</td>
      <td>0.1402</td>
      <td>0.1500</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.7506</td>
      <td>0.5883</td>
      <td>0.1576</td>
      <td>0.3459</td>
      <td>0.2165</td>
      <td>0.0923</td>
      <td>0.1024</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.7419</td>
      <td>0.5818</td>
      <td>0.1519</td>
      <td>0.3136</td>
      <td>0.2046</td>
      <td>0.0723</td>
      <td>0.0790</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.7563</td>
      <td>0.5908</td>
      <td>0.1490</td>
      <td>0.3611</td>
      <td>0.2110</td>
      <td>0.0954</td>
      <td>0.1085</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.7550</td>
      <td>0.5997</td>
      <td>0.1748</td>
      <td>0.3720</td>
      <td>0.2378</td>
      <td>0.1139</td>
      <td>0.1255</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.7638</td>
      <td>0.5890</td>
      <td>0.1891</td>
      <td>0.4125</td>
      <td>0.2593</td>
      <td>0.1413</td>
      <td>0.1565</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.7613</td>
      <td>0.6240</td>
      <td>0.1633</td>
      <td>0.3904</td>
      <td>0.2303</td>
      <td>0.1163</td>
      <td>0.1318</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.7619</td>
      <td>0.5988</td>
      <td>0.1862</td>
      <td>0.4037</td>
      <td>0.2549</td>
      <td>0.1356</td>
      <td>0.1500</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.7549</td>
      <td>0.5756</td>
      <td>0.1897</td>
      <td>0.3771</td>
      <td>0.2524</td>
      <td>0.1246</td>
      <td>0.1351</td>
    </tr>
    <tr>
      <th>Mean</th>
      <td>0.7547</td>
      <td>0.5939</td>
      <td>0.1763</td>
      <td>0.3719</td>
      <td>0.2388</td>
      <td>0.1145</td>
      <td>0.1259</td>
    </tr>
    <tr>
      <th>Std</th>
      <td>0.0065</td>
      <td>0.0126</td>
      <td>0.0191</td>
      <td>0.0279</td>
      <td>0.0214</td>
      <td>0.0214</td>
      <td>0.0230</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-dcfbc557-8ff3-4ddc-b12d-ac11d9486b3f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-dcfbc557-8ff3-4ddc-b12d-ac11d9486b3f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-dcfbc557-8ff3-4ddc-b12d-ac11d9486b3f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




```python
import numpy as np
params = {
    'n_neighbors' : np.arange(0, 50, 1)
}
tunned_knn = tune_model(knn_model, custom_grid=params)
print(tunned_knn)

```



  <div id="df-b3460ed9-d903-4ed4-b39b-824b759b0e90">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Accuracy</th>
      <th>AUC</th>
      <th>Recall</th>
      <th>Prec.</th>
      <th>F1</th>
      <th>Kappa</th>
      <th>MCC</th>
    </tr>
    <tr>
      <th>Fold</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.7813</td>
      <td>0.6482</td>
      <td>0.0372</td>
      <td>0.5000</td>
      <td>0.0693</td>
      <td>0.0402</td>
      <td>0.0876</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.7807</td>
      <td>0.6436</td>
      <td>0.0315</td>
      <td>0.4783</td>
      <td>0.0591</td>
      <td>0.0330</td>
      <td>0.0759</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.7744</td>
      <td>0.6563</td>
      <td>0.0315</td>
      <td>0.3333</td>
      <td>0.0576</td>
      <td>0.0206</td>
      <td>0.0403</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.7845</td>
      <td>0.6589</td>
      <td>0.0659</td>
      <td>0.5610</td>
      <td>0.1179</td>
      <td>0.0754</td>
      <td>0.1345</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.7826</td>
      <td>0.6645</td>
      <td>0.0315</td>
      <td>0.5500</td>
      <td>0.0596</td>
      <td>0.0368</td>
      <td>0.0903</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.7794</td>
      <td>0.6477</td>
      <td>0.0544</td>
      <td>0.4634</td>
      <td>0.0974</td>
      <td>0.0539</td>
      <td>0.0961</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.7826</td>
      <td>0.6278</td>
      <td>0.0630</td>
      <td>0.5238</td>
      <td>0.1125</td>
      <td>0.0688</td>
      <td>0.1214</td>
    </tr>
    <tr>
      <th>7</th>
      <td>0.7751</td>
      <td>0.6702</td>
      <td>0.0372</td>
      <td>0.3611</td>
      <td>0.0675</td>
      <td>0.0278</td>
      <td>0.0523</td>
    </tr>
    <tr>
      <th>8</th>
      <td>0.7813</td>
      <td>0.6409</td>
      <td>0.0630</td>
      <td>0.5000</td>
      <td>0.1120</td>
      <td>0.0662</td>
      <td>0.1146</td>
    </tr>
    <tr>
      <th>9</th>
      <td>0.7881</td>
      <td>0.6426</td>
      <td>0.0661</td>
      <td>0.6389</td>
      <td>0.1198</td>
      <td>0.0822</td>
      <td>0.1548</td>
    </tr>
    <tr>
      <th>Mean</th>
      <td>0.7810</td>
      <td>0.6501</td>
      <td>0.0482</td>
      <td>0.4910</td>
      <td>0.0873</td>
      <td>0.0505</td>
      <td>0.0968</td>
    </tr>
    <tr>
      <th>Std</th>
      <td>0.0039</td>
      <td>0.0119</td>
      <td>0.0148</td>
      <td>0.0861</td>
      <td>0.0255</td>
      <td>0.0206</td>
      <td>0.0338</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-b3460ed9-d903-4ed4-b39b-824b759b0e90')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-b3460ed9-d903-4ed4-b39b-824b759b0e90 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-b3460ed9-d903-4ed4-b39b-824b759b0e90');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>



    KNeighborsClassifier(algorithm='auto', leaf_size=30, metric='minkowski',
                         metric_params=None, n_jobs=-1, n_neighbors=42, p=2,
                         weights='uniform')
    


```python
plot_model(tunned_knn, plot = 'auc')
```


    
![png](/images/0705/output_17_0.png)
    


- AUC
  + 최소 0.5, 최고 1
  + 좋은 모델은 0.8 이상
- ROC
  + 면적


```python
# 의사결정 트리
# plot_model(tunned_knn, plot = 'feature')
plot_model(tunned_knn, plot='confusion_matrix')
```


    
![png](/images/0705/output_19_0.png)
    



```python
evaluate_model(tunned_knn)
# 최고의 모델을 찾는 것 보다는 필요한 모델의 그래프를 비교할 때 사용
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>




    interactive(children=(ToggleButtons(description='Plot Type:', icons=('',), options=(('Hyperparameters', 'param…



```python
models()
```



<script src="/static/components/requirejs/require.js"></script>
<script>
  requirejs.config({
    paths: {
      base: '/static/base',
      plotly: 'https://cdn.plot.ly/plotly-latest.min.js?noext',
    },
  });
</script>







  <div id="df-d12a53d1-70cd-4e9e-bc39-3807e72a559f">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Reference</th>
      <th>Turbo</th>
    </tr>
    <tr>
      <th>ID</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>lr</th>
      <td>Logistic Regression</td>
      <td>sklearn.linear_model._logistic.LogisticRegression</td>
      <td>True</td>
    </tr>
    <tr>
      <th>knn</th>
      <td>K Neighbors Classifier</td>
      <td>sklearn.neighbors._classification.KNeighborsCl...</td>
      <td>True</td>
    </tr>
    <tr>
      <th>nb</th>
      <td>Naive Bayes</td>
      <td>sklearn.naive_bayes.GaussianNB</td>
      <td>True</td>
    </tr>
    <tr>
      <th>dt</th>
      <td>Decision Tree Classifier</td>
      <td>sklearn.tree._classes.DecisionTreeClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>svm</th>
      <td>SVM - Linear Kernel</td>
      <td>sklearn.linear_model._stochastic_gradient.SGDC...</td>
      <td>True</td>
    </tr>
    <tr>
      <th>rbfsvm</th>
      <td>SVM - Radial Kernel</td>
      <td>sklearn.svm._classes.SVC</td>
      <td>False</td>
    </tr>
    <tr>
      <th>gpc</th>
      <td>Gaussian Process Classifier</td>
      <td>sklearn.gaussian_process._gpc.GaussianProcessC...</td>
      <td>False</td>
    </tr>
    <tr>
      <th>mlp</th>
      <td>MLP Classifier</td>
      <td>sklearn.neural_network._multilayer_perceptron....</td>
      <td>False</td>
    </tr>
    <tr>
      <th>ridge</th>
      <td>Ridge Classifier</td>
      <td>sklearn.linear_model._ridge.RidgeClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>rf</th>
      <td>Random Forest Classifier</td>
      <td>sklearn.ensemble._forest.RandomForestClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>qda</th>
      <td>Quadratic Discriminant Analysis</td>
      <td>sklearn.discriminant_analysis.QuadraticDiscrim...</td>
      <td>True</td>
    </tr>
    <tr>
      <th>ada</th>
      <td>Ada Boost Classifier</td>
      <td>sklearn.ensemble._weight_boosting.AdaBoostClas...</td>
      <td>True</td>
    </tr>
    <tr>
      <th>gbc</th>
      <td>Gradient Boosting Classifier</td>
      <td>sklearn.ensemble._gb.GradientBoostingClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>lda</th>
      <td>Linear Discriminant Analysis</td>
      <td>sklearn.discriminant_analysis.LinearDiscrimina...</td>
      <td>True</td>
    </tr>
    <tr>
      <th>et</th>
      <td>Extra Trees Classifier</td>
      <td>sklearn.ensemble._forest.ExtraTreesClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>lightgbm</th>
      <td>Light Gradient Boosting Machine</td>
      <td>lightgbm.sklearn.LGBMClassifier</td>
      <td>True</td>
    </tr>
    <tr>
      <th>dummy</th>
      <td>Dummy Classifier</td>
      <td>sklearn.dummy.DummyClassifier</td>
      <td>True</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d12a53d1-70cd-4e9e-bc39-3807e72a559f')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d12a53d1-70cd-4e9e-bc39-3807e72a559f button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d12a53d1-70cd-4e9e-bc39-3807e72a559f');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>



