# Avellaneda - Stoikov approch
### Текущий подход тестируется по данным ETHUSDT с дискретностью 1 мин в целях тестов и настроек алгоритмов



По модели Avellaneda-Stoikov делается расчет 
- резервированная цена
$$r = S_t -q\gamma\sigma^2(T-t)$$
- спред
$$\delta_a + \delta_b = \gamma\sigma^2(T-t) + \frac{1}{\gamma}\ln(1+\frac{\gamma}{k})$$

### Список параметров оптимизации (ищем RL методами)
- $\gamma$ - уровень аверсии (ниприятия) к риску
- k - параметр интенсивности сделок, который находится из соотношения $\lambda(\delta) = A\exp(-k\delta)$ ( если не находим этот параметр из реальных данных)
- $\Delta\sigma$ поправку в волатильность. Здесь мы принимаем, что $\sigma = \hat\sigma + \Delta\sigma$, где $\hat\sigma$ оценка волатильности из данных

### TODO:

#### Какие еще параметры можем оптимизировать
- T - время горизонта. Оптимизация как функция данных
- T = T(UTC time, day of week, day of year). Оптимизация как функция времени торгов
- $\Delta k$ поправку в параметр. Здесь мы принимаем, что $k = \hat{k} + \Delta k$, где $\hat{k}$ оценка параметра из данных

#### Использование модели Метона со скачками (или других классов моделей) для более эффективного нахождения начальных условий
Для модели Мертона со скачками, дифференциальное уравнение и резервированная цена:

$$ dS_t = \mu dt +\sigma dW +JdN_t$$

$$r = S_t -q\gamma\sigma^2 (T-t) - \lambda \mathbb{E}\[e^{-\gamma J} - 1\](T-t)$$

#### Использовать модель задержек подбором на основе данных

#### В качестве наблюдения подавать агенту снепшоты стакана 

## Тетради с решениями:  
### Av_Stoikov_RL
Решение первого приближения  

Оптимизируемые параметры  

- $\gamma$  
Задержка

- 1 мин  
Алгортмы RL
 
- Deep Q Learning  
- Actor Critic

### Av_Stoikov_RL_not_latency  
Решение первого приближения  
Оптимизируемые параметры     
- $\gamma$   
Задержка

- нет
  
Алгортмы RL

- Deep Q Learning  
- Actor Critic

### Av_Stoikov_RL_ gam_k 
Добавили параметр k и RL алгоритм PPO  

Оптимизируемые параметры    

- $\gamma$
- k
  
Задержка

- нет
  
Алгортмы RL

- Deep Q Learning   
- Actor Critic
- Proximal Policy Optimization

### Av_Stoikov_RL_gam_k_Dsig 
Добавили поправку в параметр $\sigma $

$$ \Delta\sigma = \sigma - \hat{\sigma} $$

где  
$\hat{\sigma} - оценка  \sigma $

Оптимизируемые параметры    

- $\gamma$
- k
- $\Delta\sigma$
  
Задержка

- нет
  
Алгортмы RL

- Deep Q Learning   
- Actor Critic
- Proximal Policy Optimization

### Av_Stoikov_RL_ gam_k_Dsig_16 
В подходе Av_Stoikov_RL_gam_k_Dsig добавили lookback до 16 значений доходностей


### Av_Stoikov_RL_ gam_k_Dsig_16_conv 
В подходе Av_Stoikov_RL_gam_k_Dsig_16 сделана замена полносвязных слоев на свертки

### Av_Stoikov_RL_ gam_k_Dsig_16_conv_DDPG 
Добавлены непрерывные действия (выбор из непрерывного пространства действий)


