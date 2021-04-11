# Cal-Num-UNPSJB


Algoritmos en Python de la Materia de Cálculo Numérico - Universidad Nacional de la Patagonia (Sede: Comodoro Rivadavia)



############# DESCOMPOSICIÓN LU ################



import numpy as np
import pprint


def lu_fac(matriz):
    A = np.array(matriz)
    epsilon = np.finfo(np.float).eps
    dims = A.shape
    L = np.zeros(dims)
    U = np.zeros(dims)
    
    for j in range(dims[0]): #pregunta la dim de la Matriz
        if abs(A[j,j]) < epsilon:   #descomposición por pivote 
            print('ERROR: pivote nulo')
            return None
        L[j,j] = 1.  # diadonal principal de L con 1, para que la descomposición sea única
        for i in range(j+1,dims[0]):
            L[i,j] = A[i,j]/A[j,j]  # descomposiciín de L
            for k in range(j+1,dims[0]):
                A[i,k] = A[i,k] - L[i,j]*A[j,k]  #descomposicion U
        for k in range(j,dims[0]):
            U[j,k] = A[j,k] #gurda los valores en el array U
    
    return L, U

# Ejercicion 1

A = [[-1,1,0,-3],[1,0,3,1],[0,1,-1,-1],[3,0,1,2] ] #Matriz del ejercicio 1
L, U = lu_fac(A)
print('L = ')
pprint.pprint(L) #imprime en forma de matriz L
print('U = ')
pprint.pprint(U) #imprime en forma de matriz U
print('L * U =')
pprint.pprint(np.dot(L,U)) #producto de la matriz L*U
print("Verificación:")
pprint.pprint(np.dot(L,U) == A) #Verificación lógica de los resultados
