%((9.8*68.1)*(1-exp(-(x*10/68.1))))/x-40

clear all
clc

fprintf('\nMÉTODOS NUMÉRICOS - 1°Práctica')
fprintf('\nMÉTODO DE LA BISECCIÓN\n\n')

%Variables de entrada:
f=input('Introduzca la función: ','s');
f=inline(f);
xu=input('Digite el límite inferior: ');
xl=input('Digite el límite superior: ');
es=input('¿Error estimado?: ');
imax=input('¿Cantidad máxima de iteraciones?: ');%salida de emergencia

%Et=error verdadero
%Ea=error aproximado absoluto
%ea=error aproximado porcentual
%Cuando el error relativo aproximado es menor que 
%el error fijado: converge

iter=0;
ea=1; %ea=abs((xu-xl)/(xu+xl))*100
xr=0;
while (iter<=imax)&&(ea>es)
    xrold=xr;
    xr=(xl+xu)/2;
    iter=iter+1;
    if xr~=0
        ea=abs(((xrold-xr)/xr)*100);
    end
    R=f(xl)*f(xr);
    if R>0
        xl=xr;
    elseif R<0
        xu=xr;
    else
        ea=0;
    end
    disp([ea,xr,iter])
end

fprintf('La raiz es : %3.6f\n',xr) %VarS
fprintf('El error aproximado es %3.6f\n',ea) %VarS
fprintf('La cantidad de iteraciones es %d\n',iter)
