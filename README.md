python
複製程式碼
import pandas as pd
import matplotlib.pyplot as plt

# 读取CSV文件
file_path = '/path/to/your/ftx_data.csv'  # 确保路径正确
data = pd.read_csv(file_path)

# 将日期列转换为日期时间格式
data['date'] = pd.to_datetime(data['date'])

# 设置日期列为索引
data.set_index('date', inplace=True)

# 绘制价格走势图
plt.figure(figsize=(14, 7))

# 绘制价格折线图
plt.plot(data.index, data['price'], label='Price', color='red')

# 标注最高点和最低点
max_price = data['price'].max()
min_price = data['price'].min()
max_price_date = data['price'].idxmax()
min_price_date = data['price'].idxmin()

plt.scatter([max_price_date], [max_price], color='green', label=f'High {max_price:.6f}', zorder=5)
plt.scatter([min_price_date], [min_price], color='red', label=f'Low {min_price:.6f}', zorder=5)

# 添加文本注释
plt.text(max_price_date, max_price, ' 高點', verticalalignment='bottom', horizontalalignment='right', color='green', fontsize=10)
plt.text(min_price_date, min_price, ' 低點', verticalalignment='top', horizontalalignment='right', color='red', fontsize=10)

# 设置标题和标签
plt.title('FTX 價格 FTT')
plt.xlabel('Date')
plt.ylabel('Price')
plt.legend()

# 显示网格
plt.grid(True)

# 显示图表
plt.show()
