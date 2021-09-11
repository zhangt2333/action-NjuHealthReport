<div align="center">
<h1 align="center">自动健康填报助手</h1>
</div>

## 简介

每天 19:30 GMT+8 自动完成体温上报，如想修改定时运行的时间，可修改 `.github/workflows/healthReport.yml` 中 `schedule` 属性。

**如果当日有异常，请手动在 APP 端填写！！！！！！！！！！！！**

## Github Actions 启用步骤

### 1. Fork 本项目

Fork 本项目: [zhangt2333/actions-NjuHealthReport](https://github.com/zhangt2333/actions-NjuHealthReport) (Star 自然是更好)

### 2. 准备需要的参数

```
{
    # fill them:
    'username': 'fill-it',  # 学号
    'password': 'fill-it',  # 密码
    'location': 'fill-it',  # 地址, 如 中国xx省xx市xx区xxxx
    'deadline': '2021-10-05', # 填报截止日期，超过该天则停止填报并报错到 actions，开区间

    'none': 'none'
}
```

### 3. 启用 Github Actions

![image-20210216140844300](README/image-20210216140844300.png)

### 4. 将参数填到 Secrets

将填好的参数加入到 Secrets 中，name 为 `DATA`，value 为步骤 2 中的多行字符串

![image-20210216140557947](README/image-20210216140557947.png)

## 为多人打卡

1. 依照 `Github Actions 启用步骤` 第 2、4 步，添加新的 Secret，假设命名为 `DATA2`  

2. 复制一遍 `.github/workflows/healthReport.yml` 中最后一行 `python health_report_helper/main.py "${{ secrets.DATA }}"` 并将其中的 `secrets.DATA` 中的 `DATA` 改为新 secrets 的键值。

3. 修改后的文件应如下所示（假设新键为`DATA2`）

```
  // .....
  - name: Run Spider
        run: |
          python health_report_helper/main.py "${{ secrets.DATA }}"
          python health_report_helper/main.py "${{ secrets.DATA2 }}"
```
