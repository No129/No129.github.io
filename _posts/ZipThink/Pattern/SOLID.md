# SOLID 
* SRP：單一職責原則
* OCP：開放封閉原則
* LSP：李氏替換原則
* ISP：介面隔離原則
* DIP：依賴反轉原則

五個原則共同要解決的都是「改變」這件事，在無法預期改變如何發生的前題下，降低改變對程序的影響。

透過「擴充」避免使用「修改」。

# SRP, Single Response principle
當改變發生時，降低受影響的類別數量。

# OCP, Open-Close principle
接受「擴充」式的改變，避免「修改」式的改變

# LSP, Liskov Substitution principle
接受「擴充」子類別來提供改變，原來使用父類別的部分不受影響

# ISP, Interface-Segregation principle
接受「擴充」實做來提供改變。

# DIP, Dependency Inversion Principle
接受「擴充」低階，避免修改高階。