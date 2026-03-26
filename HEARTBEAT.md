name: Heartbeat Loop

on:
  schedule:
    - cron: '*/10 * * * *'  # 每 10 分鐘跳一次
  workflow_dispatch:       # 讓你隨時可以點按鈕手動測試

jobs:
  heartbeat:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Update Heartbeat
        run: |
          date > HEARTBEAT.md
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git add HEARTBEAT.md
          git commit -m "Heartbeat update: $(date)"
          git push
