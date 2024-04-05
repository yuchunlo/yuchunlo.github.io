---
layout: post
title: How's the business going?
description: Present revenue of Taiwan's listed companies with a bubble chart in Python.
date: 2024-04-05
permalink: /hows-the-business-going-in-2023/
---

The annual financial statement announcements for TWSE and TPEx companies were due 1 April. Here is a bubble chart displaying the revenue, gross profit, and net profit of the 1,800+ listed profitable companies. Logarithmic axes offer a deeper dive into the details.

{% include RevenueRanking_1953_05042024.html %}

<details markdown='block'>
  <summary>The dirty little Python script for this bubble chart.</summary>

  ```python
  import numpy as np
  import pandas as pd
  import plotly.express as px
  import plotly.graph_objects as go
  import os
  import sys

  def fig_html_gen(fig, gType):
      from datetime import datetime
      import plotly.io as pio

      file_time = datetime.now().strftime('%H%M_%d%m%Y')
      pio.write_html(fig, file=rf'{gType}_{file_time}.html', auto_open=True)

  def revenue_rank():
      csv_folder_path = input('Please enter the folder path for the csv files: ')
      csv_name_list = ['StockList', 't51sb01']
      df_list = []
      encodings = ['utf-8', 'big5hkscs', 'ISO-8859-1', 'latin-1', 'cp1252', 'utf-16']
      for i in csv_name_list:
          csv_files = [file for file in os.listdir(csv_folder_path) if file.endswith('.csv') and file.startswith(i)]
          dfs = []
          for csv_file in csv_files:
              for encoding in encodings:
                  try:
                      df = pd.read_csv(os.path.join(csv_folder_path, csv_file), thousands=',', encoding=encoding)
                      break
                  except UnicodeDecodeError:
                      continue
              dfs.append(df)
          combined_df = pd.concat(dfs)
          df_list.append(combined_df)

      column_rename_dict = {'公司代號': 'symbol', '產業類別': 'industry', '英文簡稱': 'english_name', '代號': 'symbol', '名稱': 'chinese_name', '營收(億)': 'revenue', '毛利(億)': 'gross_profit', '淨利(億)': 'net_profit'}
      df_list = [df.rename(columns=column_rename_dict) for df in df_list]
      df_list[0]['symbol'] = df_list[0]['symbol'].replace({r'="(.*)"$': r'\1'}, regex=True).astype(str)
      df_list[1]['symbol'] = df_list[1]['symbol'].astype(str)
      combined_df = pd.merge(df_list[0], df_list[1], on='symbol')
      combined_df['name'] = combined_df['english_name'] + ' / ' + combined_df['chinese_name']

      df_bubble = combined_df[combined_df['revenue'] > 0].copy()
      fig_bubble = px.scatter(df_bubble, x='gross_profit', y='net_profit', size='revenue', hover_name='name')
      fig_bubble['data'][0]['marker']['sizeref'] = 7
      fig_bubble['data'][0]['marker']['color'] = 'black'
      fig_bubble['layout']['updatemenus'] = [{'type': 'buttons', 'buttons': [
          dict(label='Linear', method='relayout', args=[{'xaxis.type': 'linear', 'yaxis.type': 'linear'}]), 
          dict(label='Log', method='relayout', args=[{'xaxis.type': 'log', 'yaxis.type': 'log'}]), 
      ]}]
      fig_html_gen(fig_bubble, 'RevenueRanking')

  if __name__ == '__main__':
      revenue_rank()
  ```
</details>
