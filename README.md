# Python-Excel
Using python to connect the excel and deployment in Server 
![image](https://github.com/user-attachments/assets/5b2ca1e3-227d-4671-9060-46dec6402ab0)

# IMPORTAR BIBLIOTECAS 
import pandas as pd
import numpy as ny
import openpyxl as op

# LER ARQUIVOS
df = pd.read_excel("D:/CURSOS/PythonCurso/Chicago_Crime_Data..xlsx")


# LER ARQUIVOS
df = pd.read_excel("D:/CURSOS/PythonCurso/Chicago_Crime_Data..xlsx",engine='openpyxl')

# LER SEGUNDO ARQUIVOS
df1 = pd.read_excel("D:/CURSOS/PythonCurso/Chicago_Public_Schools_-_Progress_Report_Cards__2011-2012.xlsx",engine='openpyxl')


resultado = pd.merge_ordered(df1[['ID','Unnamed: 1']], df[['ID','DATE','CASE_NUMBER']], on='ID', how='right')


print(resultado)


#completo para  inserir no SERVIDOR
import pandas as pd
from sqlalchemy import create_engine

# Configurações do arquivo Excel e da conexão com o banco de dados
file_path = 'D:/CURSOS/PythonCurso/resultado..xlsx'
user = 'root'
password = ''
host = 'localhost'   # ou o IP do seu servidor MySQL
database = 'testes'
table_name = 'TestesPuthon'

# Ler o arquivo Excel
resultado = pd.read_excel('D:/CURSOS/PythonCurso/resultado..xlsx')

# Conectar ao banco de dados MySQL
engine = create_engine(f'mysql+mysqlconnector://{user}:{password}@{host}/{database}')

# Inserir os dados no MySQL
resultado.to_sql(name=table_name, con=engine, if_exists='append', index=False)

print("Dados inseridos com sucesso!")
