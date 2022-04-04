# Challenge - Anyone IA

<div style="text-align: center;">
  <br><br/>
  <img src="img/logo-anyone IA.png">
  <br><br/>
</div>

Los clientes y los pedidos son el alma de cualquier negocio y está prácticamente garantizado que en un momento u otro de su futuro empleo tendrá que lidiar con situaciones como la que se presenta aquí.

El archivo **customers.csv** tiene 5 columnas ( CustomerId, First Name, Last Name, City and State ). y representa los datos de los clientes.

<div style="text-align: center;">
  <br><br/>
  <img src="img/customers.PNG">
  <br><br/>
</div>

El archivo **orders.csv** tiene 6 columnas ( CustomerID, OrderID, Date, OrderTotal, ProductName, Price ). Y representa la contiene los datos de los pedidos de los clientes de customers.csv:

<div style="text-align: center;">
  <br><br/>
  <img src="img/orders.PNG">
  <br><br/>
</div>

***

Utilizamos la libreria requets para obtener la data desde el github.

```python
import requests

def import_data_files():
  r = requests.get('https://raw.githubusercontent.com/anyoneai/notebooks/main/customers_and_orders/data/customers.csv')
  with open('./sample_data/customers.csv', 'wb') as f:
    f.write(r.content)

  r = requests.get('https://raw.githubusercontent.com/anyoneai/notebooks/main/customers_and_orders/data/orders.csv')
  with open('./sample_data/orders.csv', 'wb') as f:
    f.write(r.content)
  
import_data_files()
```
***

## **Question #1.1**: How many unique orders are in the orders.csv file?

```python
import pandas as pd

df = pd.read_csv(datafile)

df_OrderID_unique = pd.unique(df['OrderID'])

print("Pedidos unicos : ",len(df_OrderID_unique))
```

***Cantidad de clientes unicos en el archivo orders.csv : 602***

***

## **Question #1.2:** In how many different states do the customers live in?


```python
import pandas as pd

df = pd.read_csv(datafile)

def corregir_campo(x):
  x_upper = x.upper()
  characters = " "
  x_upper = ''.join( x for x in x_upper if x not in characters)
  return x_upper

df_state_clear=df['State'].apply(corregir_campo)

state_unique = pd.unique(df_state_clear)

print(state_unique)
print("Cantidad de estados : ",len(state_unique),'\n')
```

***Lista de estados donde viven los clientes : ['CA' 'AZ' 'NV' 'FL' 'WA' 'NH' 'ID' 'CO' 'TX' 'NM' 'OR' 'UT' 'MA' 'IN']***

***Cantidad de estado : 14***

***

## **Question #1.3:** What is the state with most customers?


```python
import pandas as pd

df = pd.read_csv(datafile)

def corregir_campo(x):
  x_upper = x.upper()
  characters = " "
  x_upper = ''.join( x for x in x_upper if x not in characters)
  return x_upper

df_state_clear=df['State'].apply(corregir_campo)

state_maximo = df_state_clear.value_counts().idxmax()

print("Estado con mayoria de clientes : " , state_maximo)
```

***Estado con mayoria de clientes :  CA***

***

## **Question #1.4:** What is the state with the least customers?


```python
import pandas as pd

df = pd.read_csv(datafile)

def corregir_campo(x):
  x_upper = x.upper()
  characters = " "
  x_upper = ''.join( x for x in x_upper if x not in characters)
  return x_upper

df_state_clear=df['State'].apply(corregir_campo)

state_counts = df_state_clear.value_counts()

state_min= state_counts[ state_counts == state_counts.min() ]


print( "Estado con menos clientes : " , list(state_min.index) )
```

***Estado con menos clientes :  ['WA', 'NH', 'ID', 'OR', 'MA', 'IN']***

***

## **Question #1.5:** What is the most common last name?


```python
import pandas as pd

df = pd.read_csv(datafile)

LastName_unique = df['LastName'].map(lambda x:x.upper())
LastName_max = LastName_unique.value_counts().idxmax()

print( "Apellido mas comun : ", LastName_max )
```

***Apellido mas comun :  SMITH***

***

