# AWS-cheat-sheet
快速连接 AWS 并开始工作，这里以 kaggle 猫狗大战比赛为例。

### Amazon EC2 常见问题
https://aws.amazon.com/cn/ec2/faqs/#spot-instances


### Local 📱  
### Server 🛰   


```bash
#📱连接 aws
ssh -i ~/Documents/keys/awsdl.pem ubuntu@34.201.13.19


#可选
#🛰miniconda
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh


#可选
#🛰create conda env
conda install python=3.6
conda create --name dl


#可选
#🛰激活环境
source activate tensorflow_p36


#🛰常用 lib
pip install --upgrade pip
pip install -U numpy pandas sklearn matplotlib seaborn h5py==2.8.0rc1 opencv-python jupyter pillow tensorflow-gpu keras pydot-ng tqdm kaggle
sudo apt install graphviz


#可选
#🛰删除该文件中重复的两行，解除 warning
vim .config/matplotlib/matplotlibr


#可选
#🛰新建目录存放证书
mkdir cer
#📱生成 cert，并按照下面命令中的目录放置 key 和 crt
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout mykey.key -out mycert.crt -subj "/CN=local.com" -days 365


#可选
#📱scp cert
scp -i ~/Documents/keys/awsdl.pem ~/Documents/keys/mycert.crt ubuntu@34.201.13.197:cer/mycert.crt
scp -i ~/Documents/keys/awsdl.pem ~/Documents/keys/mykey.key ubuntu@34.201.13.197:cer/mykey.key


#kaggle json
#🛰生成 kaggle 默认所需文件目录
kaggle
#📱上传 token，token 需要在 kaggle 网站生成 https://github.com/Kaggle/kaggle-api#api-credentials
scp -i ~/Documents/keys/awsdl.pem ~/Downloads/kaggle.json ubuntu@34.201.13.19:.kaggle/kaggle.json
#🛰修改文件权限
chmod 600 /home/ubuntu/.kaggle/kaggle.json
mkdir catvsdog # 新建工作目录
cd catvsdog
#🛰在 catvsdog  目录下让服务器下载数据集
kaggle competitions download -c dogs-vs-cats-redux-kernels-edition -w


#🛰连接 jupyter
jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --certfile=/home/ubuntu/cer/mycert.crt --keyfile=/home/ubuntu/cer/mykey.key
#将得到链接http://localhost:8888/?token=966bcbb9f641c05d183bf27b2ed8f9e1cd211560880aaea7
#修改 localhost 为 aws 公网 IP，比如这里是34.201.13.19，在📱中打开
#第一次可以 logout 一次，创建 notebook 密码


#🐵start coding...


#🛰提交 kaggle
kaggle competitions submit -c dogs-vs-cats-redux-kernels-edition -f pred.csv -m "commit"
```
