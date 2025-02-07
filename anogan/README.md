## AnoGan Model를 이용하여 Detection하기  

## Code Reference  

[https://github.com/GunhoChoi/AnoGAN-Pytorch/blob/master/Mnist_version/AnoGAN_MNIST.ipynb](https://github.com/GunhoChoi/AnoGAN-Pytorch/blob/master/Mnist_version/AnoGAN_MNIST.ipynb)

### 간략한 모델 설명  

<img width = '500' src = 'https://user-images.githubusercontent.com/55014424/119292372-37593000-bc8b-11eb-81b3-a616b7ad45db.png'>  

*  DCGAN을 이용하여 먼저 정상데이터에 관해 학습 진행  
*  정상데이터라고 한다면 여기에서는 숫자 '0'인 데이터를 말하고 Anomaly Data의 경우에는 나머지 숫자 데이터를 의미  
``` python  
config = {
    "normal_num": 0, # 정상데이터를 의미하는 숫자
    "ratio": 0.1, # Test시에 Anomaly Data의 비율  
    "batch_size": 65,
    'epoch': 200,
    'learning_rate': 0.0002,
    'download': True # MNIST를 다운할 것인지
}
```  
*  DCGAN이 정상 데이터(숫자 0)로 학습이 먼저 잘 이루어진 후에, Test시에 Anomaly Score로 비교   
 
0이 아닌 숫자(Anomaly) : High Anomaly Score, Latent Space상에서 Coefficient를 잘 찾아가지 못할 것으로 예상   
0인 숫자(Normal) : Low Anomaly Score, Latent Space상에서 Coefficient를 잘 찾아갈 것으로 예상   


* Anomaly Score

<img width = '300' src = 'https://user-images.githubusercontent.com/55014424/119292942-5efcc800-bc8c-11eb-8f41-5a70cc86ea63.png'>  

**Residual Loss** + **Discrimination Loss**

### Result  

|AUC|Recall|Precision|F1 Score|  
|:---:|:---:|:---:|:---:|  
|0.95|0.892857|0.99|0.94|

(ROC Curve를 이용하여 Threshold 설정)  

* ROC Curve  
  
<img width = '300' src = 'https://user-images.githubusercontent.com/55014424/120881533-b85de300-c60c-11eb-98be-65bbd9562111.png'>  


#### 0이 아닌 숫자 Generate  

<p>  
    
<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/119293266-0417a080-bc8d-11eb-8f7d-89aab0b52bce.png'>  

<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/119293329-28737d00-bc8d-11eb-8890-3c14a98e46a0.png'>  

</p>  

#### 0의 숫자를 Generate  

<p>  
    
<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/119293408-55c02b00-bc8d-11eb-84a1-d93bdc7e1741.png'>

<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/119293448-6670a100-bc8d-11eb-8529-e86f2af378f6.png'>  

</p>

#### 비정상(0이 아닌 숫자)인데 정상(0)이라고 판별한 사진  

<p>
    
<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/120881765-77ff6480-c60e-11eb-8a3c-55f4fb7c415c.png'>

<img width = '100' src = 'https://user-images.githubusercontent.com/55014424/120881779-88174400-c60e-11eb-8164-51e3a7281384.png'>  
    
    
