# Ubantu
1分区建议:  
* swap 16G:交换  
* /boot  4G:引导+系统更新  
* /home 256-175类似win中的user，用户数据存储  
* /     50G:相当于win C盘，挂载home以外的杂项  
* 70-256=-186  
* 先分逻辑分区后面在分主分区,一般/Home与/分区比1:10或3:10，看个人使用环境。  
* /home 这个一定要自己分区因为这个是保存的个人数据,万一系统出问题了 这一块里面的数据还能找回来 就和windows 的d,e,f盘一样  

>>>linux study…

