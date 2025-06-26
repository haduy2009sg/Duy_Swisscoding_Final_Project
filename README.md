# <div align="center"> $\color{green}{\text {⭐Đánh giá sơ bộ giá xăng dầu Việt Nam giai đoạn 2018-2022⭐}}$

## 1. Mục tiêu

Đánh giá được yếu tố ảnh hưởng của dịch bệnh Covid-19 và chiến sự Nga-Ukraine tác động sao đến giá xăng dầu Việt Nam gia đoạn năm 2018-2022.
Đưa ra nhận định cá nhân về các tác động đó.

## 2. Biểu đồ phân bố giá xăng

### 2.1 Biểu đồ biến động giá xăng dầu theo thời gian

(https://github.com/haduy2009sg/Duy_Swisscoding_Final_Project/blob/8df945fc704d4dfdaf9dc32b024701f6bae084f3/Gi%C3%A1%20C%C3%A1c%20Lo%E1%BA%A1i%20X%C4%83ng%20D%E1%BA%A7u%20Theo%20Th%E1%BB%9Di%20Gian.png)

### 2.2 Phân bố giá xăng


```python
# phân bố giá xăng dầu
plt.figure(figsize=(14,9))
plt.suptitle('Bảng phân bố các loại xăng')
color_list = ['#74b9ff','#ff7675','#55efc4','#2ab7ef','#d82aef','#efc42a','#b4ef2a']
for i, a in enumerate(oil_column_name):
  axes = plt.subplot(2,2,i+1)
  sns.histplot(df[a], color=color_list[i], ax = axes, bins = 20,kde=True)
  axes.set_xlabel('Giá thành (VNĐ)')
  axes.set_ylabel('Số lần')
  axes.set_title(a, size = 12)
  axes.grid(color = 'black', linestyle = '--', linewidth = 1, axis = 'y')
plt.tight_layout(pad = 2.00)
plt.show()
```


    
![png](Copy%20of%20Duy-Final%20Project%20Swisscoding_files/Copy%20of%20Duy-Final%20Project%20Swisscoding_19_0.png)
    


### 2.3 Đánh giá Outlier


```python
# box plot
plt.figure(figsize=(8,6), dpi = 100)
plt.grid(color = 'green', linestyle = '--', linewidth = 0.8)
sns.boxplot(data= df[oil_column_name],orient='y', width = .3, linecolor='#110',
            linewidth=1.5,fliersize=10,medianprops=dict(color = "white", linewidth = 2),
            flierprops= dict(marker='*', markerfacecolor='yellow', markersize=12),notch=True)
plt.ylabel('Loại xăng dầu', size=15)
plt.xlabel('Giá xăng dầu',size=15)
plt.title('Box plot giá xăng dầu',size=20)
plt.show()
```


    
![png](Copy%20of%20Duy-Final%20Project%20Swisscoding_files/Copy%20of%20Duy-Final%20Project%20Swisscoding_21_0.png)
    



```python
# Outlier cho của xăng oil_column_name
plt.figure(figsize=(10,5))
for i, a in enumerate(oil_column_name):
  Q1 = df[a].quantile(0.25)
  Q3 = df[a].quantile(0.75)
  IQR = Q3 - Q1
  lower_bound = Q1 - 1.5 * IQR
  upper_bound = Q3 + 1.5 * IQR
  df_outliers = df[(df[a] < lower_bound) | (df[a] > upper_bound)][['Date',a]]
  plt.scatter(df_outliers['Date'],df_outliers[a], label = a)
plt.legend()
plt.title('Outlier')
plt.show()
```


    
![png](Copy%20of%20Duy-Final%20Project%20Swisscoding_files/Copy%20of%20Duy-Final%20Project%20Swisscoding_22_0.png)
    


✅ Giá 2 loại xăng là RON 95-III và E5 RON 92-II phân bố chủ yếu ở khoản giá từ 20000 VNĐ - 25000 VNĐ là chủ yếu

      ⏩ Do các chính sách điều chỉnh giá của Nhà nước Việt Nam vào 2 loại xăng phục vụ thiết yếu này.
      
        Quỹ bình ổn giá xăng dầu trước thời điểm điều hành giá xăng dầu lúc 15g00 ngày 19/06/2025 là -138,42 tỷ đồng.
        NOTE: Theo Báo cáo quỹ bình ổn giá xăng dầu ngày 19/06/2025 - PVoil

✅ Giá xăng dầu có những điểm Outlier ở ngưỡng thấp nằm ở vào thời gian từ khoảng tháng 3-4/2025 đến tháng 10-12/2020 (khoảng giá 15000 VNĐ). Những điểm nằm ở ngưỡng cao vào tháng 2/2022 - 7/2022 (khoảng giá trên 32000 VNĐ):

      ⏩ Giá xăng dầu có mức biến động mạnh như vậy:
        

        ▶ Do dịch bệnh Covid 19 trên thế giới lây lan nhanh khiến các nước phải đóng cửa mọi người hạn chế di chuyển không được ra khỏi nhà
        ↪ nhu cầu về xăng dầu giảm mạnh kéo theo giá dầu thô trên thế giới giảm mạnh vào năm đầu 2020. Từ đó giá xăng dầu ở Việt Nam về thấp.

        NOTE: Ngày 31/3/2020, Thủ tướng Chính phủ ban hành Chỉ thị số 16/CT-TTg về thực hiện các biện pháp cấp bách phòng, chống dịch COVID-19.
        Thực hiện cách ly toàn xã hội trong vòng 15 ngày kể từ 0 giờ ngày 1/4/2020 trên phạm vi toàn quốc

        ▶ Dịch bệnh Covid 19 năm 2022 được kiểm soát
        ↪ các nước mở cửa trở lại dẫn để nhu cầu xăng dầu cho vận chuyển tăng cao, cùng với sự đứt gãy trong chuỗi cung ứng trên thới giới
        ↪ giá dầu thô tăng cao ↪ giá xăng dầu trong nước tăng cao.

        NOTE: Ngày 1 tháng 10, sau gần 3 tháng áp dụng thực hiện chính sách “3 tại chỗ” (sản xuất, cách ly, ăn nghỉ tại chỗ). Các hoạt động công cộng, sản xuất không cần cách ly nhiều.
        
        ▶ Chiến sự giữa Nga-Ukaraine
        Đến tháng 4/2022 xung đột Nga-Ukaraine nổ ra căng làm tính hình giá dầu thô tồi tệ hơn. (100$/thùng vào 3/2022)
        ↪ Đẩy giá xăng dầu lên cao nhất vào tháng 7/2022.

        NOTE:
          - Nga là nước xuất khẩu dầu thô lớn thứ hai thế giới, với hệ thống đường ống Druzhba nối thẳng sang Trung Âu.
          - Ukraine sở hữu mạng cảng Biển Đen. Nơi mà 13% dầu mỏ vận chuyển bằng đường biển tới Địa Trung Hải, châu Âu và Bắc Mỹ của toàn cầu phải đi qua.
          Gián đoạn tại đây gây nên làn sóng giá dầu tăng cao.

## <font color ='red'> 3. Đánh giá tỉ trọng xuất-nhập khẩu dầu 2019-2021


```python
df_export_vietnam = df_oil_trade[(df_oil_trade['Country'] == 'Vietnam') & (df_oil_trade['Action'] == 'Export')]
df_import_vietnam = df_oil_trade[(df_oil_trade['Country'] == 'Vietnam') & (df_oil_trade['Action'] == 'Import')]
```


```python
# Danh sách năm
years_trade_oil = [2018, 2019, 2020, 2021]
# Tính tỉ trọng (theo phần trăm) cho từng năm
export_vietnam = []
import_vietnam = []
ratio_year = []

for yr in years_trade_oil:
    exp_val = df_export_vietnam[df_export_vietnam['Year'].dt.year == yr]['Trade Value'].item()
    imp_val = df_import_vietnam[df_import_vietnam['Year'].dt.year == yr]['Trade Value'].item()
    export_vietnam.append(round(exp_val/(10**9),3))
    import_vietnam.append(round(imp_val/(10**9),3))
    ratio_year.append(round((exp_val / (exp_val + imp_val)) * 100, 2))

# Vẽ stacked column chart
fig, ax = plt.subplots(figsize=(8, 8))

# Cột cho xuất khẩu (Nội tại)
ax.bar(years_trade_oil, export_vietnam,
       label='Nội tại (Xuất khẩu)',
       color='#66c2a5')

# Cột cho nhập khẩu, chồng lên xuất khẩu
ax.bar(years_trade_oil, import_vietnam,
       label='Nhập khẩu',
       bottom=export_vietnam,
       color='#fc8d62')

# Annotation: hiển thị tỉ trọng ngay trên cột
for i, yr in enumerate(years_trade_oil):
    ax.text(yr, export_vietnam[i],
            f"{ratio_year[i]:.1f}%",
            ha='center', va='center', color='black', fontsize=11)
    ax.text(yr, export_vietnam[i] + import_vietnam[i],
            f"{100-ratio_year[i]:.1f}%",
            ha='center', va='center', color='black', fontsize=11)

# Các thiết lập khác
ax.set_title('Tỉ trọng xuất - nhập khẩu xăng dầu Việt Nam (2018–2021)', fontsize=14)
ax.set_xlabel('Năm', fontsize=12)
ax.set_ylabel('Giá trị (Tỷ USD)', fontsize=12)
ax.set_xticks(years_trade_oil)
ax.set_xticklabels(years_trade_oil)
ax.legend(loc='upper center')
ax.grid(axis='y', linestyle='--', alpha=0.5)
plt.tight_layout()
plt.show()
```


    
![png](Copy%20of%20Duy-Final%20Project%20Swisscoding_files/Copy%20of%20Duy-Final%20Project%20Swisscoding_26_0.png)
    


Thấy rằng tỷ trọng xuất- nhập của Việt Nam thiên về nhập khẩu và có chiều hướng tăng qua từng năm -> giá xăng dầu phụ thuộc vào tình hình giá dầu thế giới.

⭐ Bối cảnh:

  - Nhu cầu tiêu thụ tăng nhanh sau dịch – Kinh tế hồi phục từ nửa cuối 2020, đặc biệt là quý II–III/2021, kéo theo nhu cầu xăng dầu cho vận tải, công nghiệp và xây dựng bùng nổ trở lại. Tiêu thụ xăng dầu nội địa tăng cao.

  - Nhà máy Lọc dầu Dung Quất và Nghi Sơn (Thanh Hóa) mới chỉ đáp ứng một phần nhu cầu khoản↪ cung nội địa nhỏ so với nhu cầu ngày càng lớn.

  - Giá dầu thô và xăng dầu thế giới tăng kỷ lục năm 2021 – Đẩy giá nhập khẩu bình quân năm 2021 đạt 593 USD/tấn, tăng 191 USD/tấn so với cùng kỳ năm trước, đẩy kim ngạch nhập khẩu xăng dầu vọt lên 4,14 tỷ USD, tăng 24,6% so với 2020 dù khối lượng giảm 15,5%.




```python
# Top 5 nước xuất khẩu dầu từ năm 2018-2021

for i, yr in enumerate(years_trade_oil):
  df_oil_top5_export = df_oil_trade[(df_oil_trade['Action'] == 'Export') & (df_oil_trade['Year'].dt.year == yr)].sort_values(by = 'Trade Value', ascending= False)
  print(f'Năm {yr} xuất khẩu:')
  display(df_oil_top5_export.head(5))
  print(end='\n\n')

country_list = df_oil_top5_export['Country'].head(5).tolist()
df_oil_trade_export = df_oil_trade[df_oil_trade['Action'] == 'Export']
plt.subplots(figsize=(8, 8))

labels = country_list
sizes = []
for i, a in enumerate(country_list):
  export_country = df_oil_trade_export[(df_oil_trade_export['Country'] == a) & (df_oil_trade_export['Year'].dt.year == 2021)]['Trade Value'].sum()
  ratio_country_export = export_country/(df_oil_trade_export[(df_oil_trade_export['Year'].dt.year == 2021)]['Trade Value'].sum())*100
  sizes.append(round(ratio_country_export,2))
orther_export = 100 - sum(sizes)
labels.append('Khác')
sizes.append(orther_export)
plt.pie(sizes, labels=labels, autopct='%1.2f%%', startangle=90)
plt.title('Top 5 nước xuất khẩu dầu năm 2021', fontsize=14)
plt.legend()
plt.show()
```

    Năm 2018 xuất khẩu:




  <div id="df-cbecbd8e-3e10-4b51-8937-2752d5a0871f" class="colab-df-container">
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
      <th>Continent</th>
      <th>Country</th>
      <th>Trade Value</th>
      <th>Year</th>
      <th>Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>488</th>
      <td>Asia</td>
      <td>Saudi Arabia</td>
      <td>1.658830e+11</td>
      <td>2018-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>526</th>
      <td>Europe</td>
      <td>Russia</td>
      <td>1.331150e+11</td>
      <td>2018-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>472</th>
      <td>Asia</td>
      <td>Iraq</td>
      <td>8.223727e+10</td>
      <td>2018-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>537</th>
      <td>North America</td>
      <td>Canada</td>
      <td>6.667683e+10</td>
      <td>2018-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>461</th>
      <td>Asia</td>
      <td>United Arab Emirates</td>
      <td>5.802676e+10</td>
      <td>2018-01-01</td>
      <td>Export</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-cbecbd8e-3e10-4b51-8937-2752d5a0871f')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
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

    .colab-df-buttons div {
      margin-bottom: 4px;
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
        document.querySelector('#df-cbecbd8e-3e10-4b51-8937-2752d5a0871f button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-cbecbd8e-3e10-4b51-8937-2752d5a0871f');
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


    <div id="df-6f0aaae1-185c-446c-a5de-2b8a549a6920">
      <button class="colab-df-quickchart" onclick="quickchart('df-6f0aaae1-185c-446c-a5de-2b8a549a6920')"
                title="Suggest charts"
                style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
      </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

      <script>
        async function quickchart(key) {
          const quickchartButtonEl =
            document.querySelector('#' + key + ' button');
          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
          quickchartButtonEl.classList.add('colab-df-spinner');
          try {
            const charts = await google.colab.kernel.invokeFunction(
                'suggestCharts', [key], {});
          } catch (error) {
            console.error('Error during call to suggestCharts:', error);
          }
          quickchartButtonEl.classList.remove('colab-df-spinner');
          quickchartButtonEl.classList.add('colab-df-quickchart-complete');
        }
        (() => {
          let quickchartButtonEl =
            document.querySelector('#df-6f0aaae1-185c-446c-a5de-2b8a549a6920 button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>



    
    
    Năm 2019 xuất khẩu:




  <div id="df-2585cb33-fce5-4301-8042-98af3f69cab2" class="colab-df-container">
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
      <th>Continent</th>
      <th>Country</th>
      <th>Trade Value</th>
      <th>Year</th>
      <th>Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>349</th>
      <td>Asia</td>
      <td>Saudi Arabia</td>
      <td>1.493090e+11</td>
      <td>2019-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>390</th>
      <td>Europe</td>
      <td>Russia</td>
      <td>1.231360e+11</td>
      <td>2019-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>332</th>
      <td>Asia</td>
      <td>Iraq</td>
      <td>7.472220e+10</td>
      <td>2019-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>400</th>
      <td>North America</td>
      <td>Canada</td>
      <td>6.777533e+10</td>
      <td>2019-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>411</th>
      <td>North America</td>
      <td>United States</td>
      <td>6.180260e+10</td>
      <td>2019-01-01</td>
      <td>Export</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-2585cb33-fce5-4301-8042-98af3f69cab2')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
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

    .colab-df-buttons div {
      margin-bottom: 4px;
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
        document.querySelector('#df-2585cb33-fce5-4301-8042-98af3f69cab2 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-2585cb33-fce5-4301-8042-98af3f69cab2');
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


    <div id="df-0adf96e5-2be4-4650-95b5-54ac64deecc7">
      <button class="colab-df-quickchart" onclick="quickchart('df-0adf96e5-2be4-4650-95b5-54ac64deecc7')"
                title="Suggest charts"
                style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
      </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

      <script>
        async function quickchart(key) {
          const quickchartButtonEl =
            document.querySelector('#' + key + ' button');
          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
          quickchartButtonEl.classList.add('colab-df-spinner');
          try {
            const charts = await google.colab.kernel.invokeFunction(
                'suggestCharts', [key], {});
          } catch (error) {
            console.error('Error during call to suggestCharts:', error);
          }
          quickchartButtonEl.classList.remove('colab-df-spinner');
          quickchartButtonEl.classList.add('colab-df-quickchart-complete');
        }
        (() => {
          let quickchartButtonEl =
            document.querySelector('#df-0adf96e5-2be4-4650-95b5-54ac64deecc7 button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>



    
    
    Năm 2020 xuất khẩu:




  <div id="df-b5c04c28-efeb-4b5c-b0ee-926ab4648e80" class="colab-df-container">
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
      <th>Continent</th>
      <th>Country</th>
      <th>Trade Value</th>
      <th>Year</th>
      <th>Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>206</th>
      <td>Asia</td>
      <td>Saudi Arabia</td>
      <td>9.739653e+10</td>
      <td>2020-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>246</th>
      <td>Europe</td>
      <td>Russia</td>
      <td>7.442380e+10</td>
      <td>2020-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>267</th>
      <td>North America</td>
      <td>United States</td>
      <td>5.220654e+10</td>
      <td>2020-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>256</th>
      <td>North America</td>
      <td>Canada</td>
      <td>4.717733e+10</td>
      <td>2020-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>190</th>
      <td>Asia</td>
      <td>Iraq</td>
      <td>4.540363e+10</td>
      <td>2020-01-01</td>
      <td>Export</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-b5c04c28-efeb-4b5c-b0ee-926ab4648e80')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
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

    .colab-df-buttons div {
      margin-bottom: 4px;
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
        document.querySelector('#df-b5c04c28-efeb-4b5c-b0ee-926ab4648e80 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-b5c04c28-efeb-4b5c-b0ee-926ab4648e80');
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


    <div id="df-89c1715f-d1ef-4aa7-a47e-53dbaacc676d">
      <button class="colab-df-quickchart" onclick="quickchart('df-89c1715f-d1ef-4aa7-a47e-53dbaacc676d')"
                title="Suggest charts"
                style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
      </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

      <script>
        async function quickchart(key) {
          const quickchartButtonEl =
            document.querySelector('#' + key + ' button');
          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
          quickchartButtonEl.classList.add('colab-df-spinner');
          try {
            const charts = await google.colab.kernel.invokeFunction(
                'suggestCharts', [key], {});
          } catch (error) {
            console.error('Error during call to suggestCharts:', error);
          }
          quickchartButtonEl.classList.remove('colab-df-spinner');
          quickchartButtonEl.classList.add('colab-df-quickchart-complete');
        }
        (() => {
          let quickchartButtonEl =
            document.querySelector('#df-89c1715f-d1ef-4aa7-a47e-53dbaacc676d button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>



    
    
    Năm 2021 xuất khẩu:




  <div id="df-6615ff28-d8e3-4d7a-843e-29ff9c3efd53" class="colab-df-container">
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
      <th>Continent</th>
      <th>Country</th>
      <th>Trade Value</th>
      <th>Year</th>
      <th>Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>67</th>
      <td>Asia</td>
      <td>Saudi Arabia</td>
      <td>1.376140e+11</td>
      <td>2021-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>110</th>
      <td>Europe</td>
      <td>Russia</td>
      <td>1.126830e+11</td>
      <td>2021-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>119</th>
      <td>North America</td>
      <td>Canada</td>
      <td>8.122881e+10</td>
      <td>2021-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>49</th>
      <td>Asia</td>
      <td>Iraq</td>
      <td>7.204987e+10</td>
      <td>2021-01-01</td>
      <td>Export</td>
    </tr>
    <tr>
      <th>131</th>
      <td>North America</td>
      <td>United States</td>
      <td>6.763051e+10</td>
      <td>2021-01-01</td>
      <td>Export</td>
    </tr>
  </tbody>
</table>
</div>
    <div class="colab-df-buttons">

  <div class="colab-df-container">
    <button class="colab-df-convert" onclick="convertToInteractive('df-6615ff28-d8e3-4d7a-843e-29ff9c3efd53')"
            title="Convert this dataframe to an interactive table."
            style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px" viewBox="0 -960 960 960">
    <path d="M120-120v-720h720v720H120Zm60-500h600v-160H180v160Zm220 220h160v-160H400v160Zm0 220h160v-160H400v160ZM180-400h160v-160H180v160Zm440 0h160v-160H620v160ZM180-180h160v-160H180v160Zm440 0h160v-160H620v160Z"/>
  </svg>
    </button>

  <style>
    .colab-df-container {
      display:flex;
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

    .colab-df-buttons div {
      margin-bottom: 4px;
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
        document.querySelector('#df-6615ff28-d8e3-4d7a-843e-29ff9c3efd53 button.colab-df-convert');
      buttonEl.style.display =
        google.colab.kernel.accessAllowed ? 'block' : 'none';

      async function convertToInteractive(key) {
        const element = document.querySelector('#df-6615ff28-d8e3-4d7a-843e-29ff9c3efd53');
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


    <div id="df-bcdcfccc-50ab-448a-9701-8e4c36952f11">
      <button class="colab-df-quickchart" onclick="quickchart('df-bcdcfccc-50ab-448a-9701-8e4c36952f11')"
                title="Suggest charts"
                style="display:none;">

<svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
     width="24px">
    <g>
        <path d="M19 3H5c-1.1 0-2 .9-2 2v14c0 1.1.9 2 2 2h14c1.1 0 2-.9 2-2V5c0-1.1-.9-2-2-2zM9 17H7v-7h2v7zm4 0h-2V7h2v10zm4 0h-2v-4h2v4z"/>
    </g>
</svg>
      </button>

<style>
  .colab-df-quickchart {
      --bg-color: #E8F0FE;
      --fill-color: #1967D2;
      --hover-bg-color: #E2EBFA;
      --hover-fill-color: #174EA6;
      --disabled-fill-color: #AAA;
      --disabled-bg-color: #DDD;
  }

  [theme=dark] .colab-df-quickchart {
      --bg-color: #3B4455;
      --fill-color: #D2E3FC;
      --hover-bg-color: #434B5C;
      --hover-fill-color: #FFFFFF;
      --disabled-bg-color: #3B4455;
      --disabled-fill-color: #666;
  }

  .colab-df-quickchart {
    background-color: var(--bg-color);
    border: none;
    border-radius: 50%;
    cursor: pointer;
    display: none;
    fill: var(--fill-color);
    height: 32px;
    padding: 0;
    width: 32px;
  }

  .colab-df-quickchart:hover {
    background-color: var(--hover-bg-color);
    box-shadow: 0 1px 2px rgba(60, 64, 67, 0.3), 0 1px 3px 1px rgba(60, 64, 67, 0.15);
    fill: var(--button-hover-fill-color);
  }

  .colab-df-quickchart-complete:disabled,
  .colab-df-quickchart-complete:disabled:hover {
    background-color: var(--disabled-bg-color);
    fill: var(--disabled-fill-color);
    box-shadow: none;
  }

  .colab-df-spinner {
    border: 2px solid var(--fill-color);
    border-color: transparent;
    border-bottom-color: var(--fill-color);
    animation:
      spin 1s steps(1) infinite;
  }

  @keyframes spin {
    0% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
      border-left-color: var(--fill-color);
    }
    20% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    30% {
      border-color: transparent;
      border-left-color: var(--fill-color);
      border-top-color: var(--fill-color);
      border-right-color: var(--fill-color);
    }
    40% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-top-color: var(--fill-color);
    }
    60% {
      border-color: transparent;
      border-right-color: var(--fill-color);
    }
    80% {
      border-color: transparent;
      border-right-color: var(--fill-color);
      border-bottom-color: var(--fill-color);
    }
    90% {
      border-color: transparent;
      border-bottom-color: var(--fill-color);
    }
  }
</style>

      <script>
        async function quickchart(key) {
          const quickchartButtonEl =
            document.querySelector('#' + key + ' button');
          quickchartButtonEl.disabled = true;  // To prevent multiple clicks.
          quickchartButtonEl.classList.add('colab-df-spinner');
          try {
            const charts = await google.colab.kernel.invokeFunction(
                'suggestCharts', [key], {});
          } catch (error) {
            console.error('Error during call to suggestCharts:', error);
          }
          quickchartButtonEl.classList.remove('colab-df-spinner');
          quickchartButtonEl.classList.add('colab-df-quickchart-complete');
        }
        (() => {
          let quickchartButtonEl =
            document.querySelector('#df-bcdcfccc-50ab-448a-9701-8e4c36952f11 button');
          quickchartButtonEl.style.display =
            google.colab.kernel.accessAllowed ? 'block' : 'none';
        })();
      </script>
    </div>

    </div>
  </div>



    
    



    
![png](Copy%20of%20Duy-Final%20Project%20Swisscoding_files/Copy%20of%20Duy-Final%20Project%20Swisscoding_28_9.png)
    


▶ Nga là nước xuất khẩu dầu đúng thứ hai thế giới năm 2018-2021. Tỉ trọng xuất khẩu dầu cao chiếm 11.84% xuất khẩu của thế giới năm 2021 ↪ Giá dầu thô thế giới tăng cao khi chiến sự Nga-Ukraine diễn ra vào tháng 4-2022.
    
      ❗ Giá xăng dầu việt Nam tăng cao chạm đỉnh (Giá xăng RON 95-III: 32870 VNĐ) vào thời điểm đó.

## <font color = 'red'> 4. Đánh giá tổng quá và đưa nhận định cá nhân

⭐ Kết luận:

  ▶ Thấy rằng tình hình giá xăng dầu ở Việt Nam còn phụ thuộc nhiều vào giá dầu thế giới.
  
⭐ Nhận định cá nhân:

  - Bối cảnh: Trong hiện trạng khu vực xuất khẩu dầu lớn đang ảnh hưởng bởi chiến sự và việc áp dụng lệnh trừng phạt của các nước lớn: Mỹ, liên minh châu Âu lên các khu vực này còn đẩy giá dầu thế giới tăng.
      
  ⬇ Việt Nam nên:

    1. Tăng hay hỗ trợ đầu tư vào xây dựng thêm nhà máy lọc dầu ( nhà máy lọc dầu Dung Quất hiện tại vẫn chưa đáp ứng đủ nhu cầu trong nước). Tăng tính tự chủ và đảm bảo an ninh quốc phòng.

    2. Chuyển đổi xe xăng thành xe điện giảm phụ thuộc quá nhiều vào xăng (Theo thống kê của World Atlas năm 2023 cho thấy Việt Nam là nước xếp thứ 2 thế giới về tỷ lệ hộ gia đình dùng xe máy (86%)).

    3. Đây mạnh xây dựng vận tải hành khách công cộng (hiện đang có nhưng bước chuyển tốt tại cái thành phố lớn Hà Nội và Hồ Chí Minh: đầu tư hệ thống tàu điện, xe bus chạy điện,...)

⭐ Thách thức và lợi thế:
  
1. Thách thức:

  - Đầu tư vào xe điện và xây dựng có triển khai lâu và lâu hiệu quả.
  
  - Người dân khó thay đổi thói quen di chuyển.

2. Lợi thế:

  - Do có tỉ trọng sản xuất dầu trong nước nhỏ nên khi chuyển đổi qua nhiên liệu mới dễ hơn.

  - Lợi thế cho việc đầu tư cung cấp các nguồn nhiên liệu mới thay thế xăng dầu.
