[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/911zZL51)
# calculo-numerico-exercicio-3

Informações nos slides da Aula 11 de Cálculo Numérico.

Dica: se o vetor de tempo iniciar em t(0) não nulo, é de bom tom zerar o primeiro valor e escrever em função disso.
Por exemplo: suponha que seja enviado um ```t = [1.1, 1.4, 1.6, 1.8]```. Então, você deveria fazer ```t = t-t(1)``` para que seu vetor t seja ```t=[0, 0.3, 0.5, .7]```.
%% ATIVIDADE 3 - Manuela Somoza

% Foi permitido que as bactérias crescessem tanto quanto possível nas primeiras 2,5 horas e, então, elas foram induzidas a produzir uma proteína recombi- nante, e essa produção diminui significativamente o cres- cimento bacteriano. O crescimento teórico das bactérias pode ser descrito por
% dX/dt = uX
%onde X é o número de bactérias e μ é a taxa de crescimento específico da bactéria durante o crescimento exponencial. Com base nos dados, qual a estimativa da taxa de crescimento específica da bactéria durante as primeiras 2 horas de crescimento? E durante as próximas quatro horas de crescimento?

%Considerando que as bactérias são unicelulares e que os valores dados para quantidade de célula são equivalentes para a quantidade de bactérias

T = 0:1:6;
NC = [0.100 0.332 1.102 1.644 2.453 3.650 5.460];
X = NC;

% resolvendo manualmente a EDO, temos:
% X(t) = X0 * e^(u*t)

lnX = log(X);
plot(T, lnX, 'o-');
xlabel('Tempo (h)');
ylabel('ln(X)');
grid on;

t1 = T(1:3);          % 0, 1 e 2 h
lnX1 = lnX(1:3);
p1 = polyfit(t1, lnX1, 1);
ul = p1(1);
printf('Taxa de crescimento u1 (0–2h) = %.4f h^-1\n', ul);

t2 = T(3:end);        % de 2h até 6h
lnX2 = lnX(3:end);
p2 = polyfit(t2, lnX2, 1);
u2 = p2(1);
printf('Taxa de crescimento u2 (2–6h) = %.4f h^-1\n', u2);

hold on;
plot(t1, polyval(p1, t1), 'r--', 'LineWidth', 2);  % ajuste 0–2h
plot(t2, polyval(p2, t2), 'g--', 'LineWidth', 2);  % ajuste 2–6h
legend('Dados experimentais', 'Ajuste 0–2h', 'Ajuste 2–6h', 'location', 'northwest');
title('Crescimento bacteriano - ln(X) vs Tempo');
hold off;
