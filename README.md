TASK3循环那段没注意写了两次，但是功能居然实现了，上传完了但是我好像不会修正，DS让我重新上传一个TASK3修改版（应该没事吧）
TASK1
第一遍代码是跟着铁头山羊写的：
/*user code begin while*/
while(1)
{
    HAL_GPIO_WritePin(GPIOA,GPIO_PIN_9,GPIO_PIN_RESET);
    HAL_GPIO_WritePin(GPIOC,GPIO_PIN_13,GPIO_PIN_SET);
		HAL_Delay(250);
		HAL_GPIO_WritePin(GPIOA,GPIO_PIN_9,GPIO_PIN_SET);
    HAL_GPIO_WritePin(GPIOC,GPIO_PIN_13,GPIO_PIN_RESET);
		HAL_Delay(250);
}
之后自己理解了一下就是不让板载灯亮的话就不需要PC13
while(1)
{
  HAL_GPIO_WritePin(GPIOA,GPIO_PIN_9,GPIO_PIN_RESET);
	HAL_Delay(250);
	HAL_GPIO_WritePin(GPIOA,GPIO_PIN_9,GPIO_PIN_SET);
	HAL_Delay(250);
}
或者写成HAL_GPIO_TogglePIN的形式，但是代码交了就没改

TASK2
/*begin2*/
HAL_TIM_Base_Start_IT(&gtim2)
/*end2*/
//启动定时器
/*begin4*/
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
//老大括号里的好难记（
{
  if(htim->Intense==TIM2)
    HAL_GPIO_TogglePIN(GPIOA,GPIO_PIN_9);
}
//数完了回调

TASK3
/*PV*/
volatitle uint8_t key_flag=0;
//芝士按钮
/*PV*/
/*while*/
if(key_flag)
{  
  HAL_Delay(20);
  if(HAL_GPIO_ReadPIN(GPIOA,GPIO_PIN_0)==GPIO_PIN_RESET)
    HAL_GPIO_TogglePIN(GPIOA,GPIO_PIN_9);
  key_flag=0;
}
//按键消抖，20ms后通过读A0引脚电平来翻转PA13
/*while*/
/*4*/
void HAL_EXTI_Callback(uint16_t GPIO_PIN)
{
  if(GPIO_PIN==GPIO_PIN_0)
    key_flag=1;
}
/*4*/
//按下按钮后通过A0电平回调
//readme没复制keil，手打的，应该不会打错吧

