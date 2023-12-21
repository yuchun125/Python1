import pandas as pd
import matplotlib.pyplot as plt

# 創建示例數據
data = {
    '日期': ['2023-11-01', '2023-11-02', '2023-11-03', '2023-11-04', '2023-11-05', '2023-11-06', '2023-11-07', '2023-11-08', '2023-11-09', '2023-11-10', '2023-11-11', '2023-11-12', '2023-11-13', '2023-11-14', '2023-11-15', '2023-11-16', '2023-11-17', '2023-11-18', '2023-11-19', '2023-11-20', '2023-11-21', '2023-11-22', '2023-11-23', '2023-11-24', '2023-11-25', '2023-11-26', '2023-11-27', '2023-11-28', '2023-11-29','2023-11-30'],
    '睡眠時間（小時）': [7, 8, 6, 7.5, 8.5, 5, 7, 4, 6, 9, 6, 8, 7.5, 5.5, 6, 7, 6.5, 5, 4.5, 7, 8, 5, 9, 7.5, 6, 5.5, 7, 8, 4.5, 5]
}
# 將數據轉換為DataFrame
df = pd.DataFrame(data)

# 將 '日期' 列轉換為 datetime 格式
df['日期'] = pd.to_datetime(df['日期'])

# 繪製睡眠時間折線圖
plt.figure(figsize=(10, 5))
plt.plot(df['日期'], df['睡眠時間（小時）'], marker='o', color='purple', label='睡眠時間（小時）')
plt.axhline(y=df['睡眠時間（小時）'].mean(), color='red', linestyle='--', label='平均睡眠時間')  # 添加平均線
plt.title('每日睡眠時間追蹤')
plt.xlabel('日期')
plt.ylabel('睡眠時間（小時）')
plt.legend()
plt.grid(True)
plt.xticks(rotation=45)  # 添加日期旋轉
plt.tight_layout()  # 自動調整圖表布局

# 設置 y 軸範圍
plt.ylim(0, 12)

# 顯示每個數據點的值
for i, txt in enumerate(df['睡眠時間（小時）']):
    plt.annotate(txt, (df['日期'][i], df['睡眠時間（小時）'][i]), textcoords="offset points", xytext=(0, 10), ha='center')

# 計算平均睡眠時間
average_sleep_time = df['睡眠時間（小時）'].mean()

# 打印平均睡眠時間
print(f"平均睡眠時間: {average_sleep_time}")

# 顯示中文
plt.rcParams['font.sans-serif'] = ['Microsoft YaHei']
plt.rcParams['axes.unicode_minus'] = False

# 打印DataFrame
print("健康報告：")
print(df)

# 保存數據到CSV文件
df.to_csv('health_report.csv', index=False)

# 保存睡眠時間折線圖
try:
    plt.savefig('sleep_time_chart.png')
    print("成功保存圖片：sleep_time_chart.png")
except Exception as e:
    print(f"保存圖片失敗：{e}")

# 顯示圖表
plt.show()
