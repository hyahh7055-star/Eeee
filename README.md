name: Nexus-Miner
on:
  workflow_dispatch:
jobs:
  Nexus-Job:
    runs-on: ubuntu-latest
    timeout-minutes: 360
    steps:
      - name: Download and Install Nexus
        run: |
          curl https://cli.nexus.xyz/install.sh | sh
      - name: Run Nexus Miner
        run: |
          # التسجيل التلقائي بمحفظتك لحل مشكلة Configuration file not found
          /home/runner/.nexus/bin/nexus-cli register-user --wallet-address 0x1E91136DA85630d94DC53bb74Dc53e2ce71278cc
          
          # بدء التعدين الفعلي بـ 2 Threads
          /home/runner/.nexus/bin/nexus-cli start --max-threads 2 &
      - name: Keep Alive Loop
        run: |
          while true; do
            echo "[$(date)] Nexus is actively proving for 0x1E91...cc"
            sleep 300
          done
          
