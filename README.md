# Ants
Ants ALgoritm

    import numpy as np
    import math
    import sys
    def Poisk_Pij(i,j,start,odb): # Поиск матрицы вероятности для "жадного" алгоритма 
    
    Pij=100*1/start[i][j]/sum(odb[i])
    return Pij
    
    def poisk(start,P,size):      # Поиск минимального пути, временно ограниченный размерностью
        ants=[0,1,2,3,4]          # Муравьи
        ant=0
        j=0
        i=0
        while i<size:
            ant = i
            put=0
            P_i=P.copy()
            while j<size-1:          #Создание списков Для определения следующего значения вероятности перехода для данного муравья
                P1=list(P_i[0])      #Чтобы он не ходил в город, в котором уже был
                P2=list(P_i[1])
                P3=list(P_i[2])
                P4=list(P_i[3])
                P5=list(P_i[4])
                Puts=[P1,P2,P3,P4,P5]
                indexes=[]
                for gen in Puts:
                    indexes.append(gen.index(max(gen)))
                put+=start[ant][indexes[ant]]    #Расчет самого пути муравья
                P_i[ant][indexes[ant]]=0       #Присваивание нулевой вероятности путям, по которым идти уже не надо, чтобы не вернуться обратно
                P_i[0][ant]=0
                P_i[1][ant]=0
                P_i[2][ant]=0
                P_i[3][ant]=0
                P_i[4][ant]=0
                ant=indexes[ant]
                j+=1
            put+=start[ant][i]
            ants[i]=put
            i+=1
            j=0
        return int(min(ants))  #Возврат минимального пути пройденного одним из муравьев
            
        
   
    
    
    
    np.random.seed=7
    #a=np.array([0,2,30,9,1,4,0,47,7,7,31,33,0,33,36,20,13,16,0,28,9,36,22,22,0])
    a=np.loadtxt(sys.stdin)                              #Ввод значений в матрицу а
    #size=int(math.sqrt(len(a)))
    #b=a.reshape(size,size)
    size=len(a)                                          #Взятие длины строки для последующего применения
    one_dev_b=np.zeros((size,size))
    P=np.zeros((size,size)) #Создание пустого списка для вычисления вероятности перехода 
    i=0
    j=0
    while i<size:
        while j<size:
            if i!=j:
                one_dev_b[i][j]=1/b[i][j]      #Расчет новой матрицы со значениями 1/а, кроме главной диагонали 
            j+=1
        i+=1
        j=0
    i=0
    j=0
    while i<size:
        while j<size:
            if i!=j:
                P[i][j]=Poisk_Pij(i,j,b,one_dev_b)        
            j+=1
        i+=1
        j=0
    print(poisk(b,P,size))
