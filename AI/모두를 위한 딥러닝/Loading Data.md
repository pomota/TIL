## Loading Data
### Problems of Data in real world
데이터의 방대한 양
- 너무 느림
- 하드웨어적으로 불가능
-> 일부분의 데이터로만 학습

### Minibatch Gradient Descent
전체 데이터를 균일하게 나눠서 학습하자
- 업데이트가 빨라짐
- cost 계산에 전체 데이터를 쓰지 않아 잘못된 방향으로 업데이트할 수 있음

### Pytorch Dataset
```
from torch.util.data import Dataset

class CustomDataset(Dataset): # torch.utils.data.Dataset 상
  def __init__(self):
    self.x_data = [~~~]
    self.y_data = [~~~]
  
  def __len__(self): # 총 데이터 수 반환
    return len(self.x_data)
  
  def __getitem__(self,idx): # 인덱스의 데이터를 torch tensor로 반
    x = torch.FloatTensor(self.x_data[idx])
    y = torch.FloatTensor(self.y_data[idx])
    return x, y

dataset = CustomDataset()
```

### Pytorch DataLoader
2개의 매개변수: dataset, batch_size
```
from torch.utils.data import DataLoader

dataloader = DataLoader(
  dataset,
  batch_size = 2, # 통상적으로 2의 거듭제곱
  shuffle = True,  # epoch마다 데이터셋의 순서를 섞음
)
```

### 전체코드
enumerate(dataloader): minibatch 인덱스와 데이터를 받음

len(dataloader): 한 epoch 당 minibatch 개수

```
nb_epochs = 20

for epoch in range(1, nb_epochs+1)
for batch_idx, samples in enumerate(dataloader):
x_train, y_train = samples

# H(x) 계산
prediction = model(x_train)

# cost 계산
cost = F.mse_loss(prediction, y_train)

# 학습
optimizer.zero_grad()
cost.backward()
optimizer.step()

print('Epoch {:6d}/{} Batch {}/{} Cost: {:.6f}'.format(epoch, nb_epochs, batch_idx+1, len(dataloader), cost.item()))
```


