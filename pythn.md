import pandas as pd
from patsy import dmatrices

df_original = pd.DataFrame({
   'A': ['red', 'green', 'red', 'green'],
   'B': ['car', 'car', 'truck', 'truck'],
   'C': [10,11,12,13],
   'D': ['alice', 'bob', 'charlie', 'alice']},
   index=[0, 1, 2, 3])

_, df_dummyfied = dmatrices('A ~ A + B + C + D', data=df_original, return_type='dataframe')
df_dummyfied = df_dummyfied.drop('Intercept', axis=1)

df_dummyfied.columns    
Index([u'A[T.red]', u'B[T.truck]', u'D[T.bob]', u'D[T.charlie]', u'C'], dtype='object')

df_dummyfied
   A[T.red]  B[T.truck]  D[T.bob]  D[T.charlie]     C
0       1.0         0.0       0.0           0.0  10.0
1       0.0         0.0       1.0           0.0  11.0
2       1.0         1.0       0.0           1.0  12.0
3       0.0         1.0       0.0           0.0  13.0