# Ubuntu18.04-install


# 安裝顯卡驅動
# Step 1 禁用 nouveau

終端機輸入:
lsmod | grep nouveau

//如果有輸出則表示nouveau正在加載

sudo gedit /etc/modprobe.d/blacklist.conf

//在打開文本的最後面添加：

blacklist nouveau

options nouveau modeset=0

//Save

source ~/.bashrc

reboot
(重啟後，畫面解析度會降低)
再一次查看是否有禁用nouveau成功

lsmod | grep nouveau

# Step 2 安裝NVIDIA顯示卡驅動
終端機輸入
ubuntu-drivers devices

//可查看目前可安裝的驅動版本

//nvidia-driver-410 - third-party free

//nvidia-driver-415 - third-party free

//nvidia-driver-450 - third-party free....

//選擇要安裝的版本，輸入指令 sudo apt-get install

//install 後面輸入出現的驅動名字



sudo apt-get install nvidia-driver-450

輸入nvidia-smi 檢查是否安裝成功

以上完成顯示卡驅動安裝!!!!!

# 安裝Gcc 5 & G++ 5
因为Ubuntu18.04默认gcc7.0，而CUDA9.0只支持gcc6.0及以下版本

首先查看自己的版本

gcc –version

显示7.x

在终端输入

sudo apt install gcc-5 

sudo apt install g++-5

sudo mv gcc gcc.bak

sudo ln -s gcc-5 gcc

sudo mv g++ g++.bak

sudo ln -s g++-5 g++

gcc –version

显示5.x


# 安裝CUDA 9.0
網路上搜尋nvidia CUDA，並進入CUDA安裝網頁

# Step 1
1.進入安裝網頁後，因為nvidia會自動轉入cuda最新版本的頁面，所以需要自行找尋舊版本
![Alt text](1.PNG?raw=true "Title")

2.尋找CUDA9.0的超連結
![Alt text](2.png?raw=true "Title")

3.進入CUDA9.0的頁面後，請依照OS系統(如下圖的點選)點選條件
3.1 Download
3.2 下載完檔案後，請在ubuntu尋找檔案的資料夾，並在資料夾中右鍵點開終端機，並輸入

sudo sh cuda_9.0.130_410.48_linux.run
![Alt text](3.png?raw=true "Title")

4.輸入完後會進入CUDA安裝的協議文件，可以利用鍵盤的SPACE(空白鍵)快速瀏覽

5.開始會詢問安裝的條件，除了有一個問題會詢問是否安裝driver，需要回答N以外(因為先前已經先安裝過，不需要再安裝)，其他問題基本上都是Y, accept，遇到路徑的問題，直接按下ENTER鍵，使用預設路徑

6.CUDA 安裝成功!!

7.添加環境變數

終端機輸入

sudo gedit ~/.bashrc

在文件的末端添加

export PATH=/usr/local/cuda-9.0/bin:$PATH

export LD_LIBRARY_PATH=/usr/local/cuda-9.0/lib64:$LD_LIBRARY_PATH

export CUDA_HOME=/usr/local/cuda-9.0:$CUDA_HOME

保存退出，終端運行 source ~/.bashrc

輸入nvcc -V 檢查是否安裝成功

以上完成顯示卡驅動安裝!!!!

# 安裝CUDNN 7.6.5

sudo cp cuda/include/cudnn.h /usr/local/cuda/include

sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64

sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*

