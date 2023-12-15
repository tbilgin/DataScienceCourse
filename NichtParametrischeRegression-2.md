# Nicht Parametrische Regression

Lade den Datensatz co2.csv unten. Falls du ihn unter Downloads gespeichert hast, stelle dein Arbeitsverzeichnis als Downloads ein.
<img width="815" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/e9ecec31-37b3-413a-a6a2-32d7ec02ff70">
Jetzt lade den Datensatz zum deinem Arbeitsverzeichnis:
```
co2 = read.csv("co2.csv", header = TRUE)
```
Durchsuche den Datensatz mit den üblichen Befehlen. Finde heraus, wie viele Spalten und Zeilen, und welchen Datentyp er hat.
Sind die Daten normal verteilt?
```
shapiro.test(co2$concentration)
ggplot(co2, aes(concentration)) + geom_density()
```
<img width="397" alt="Bildschirmfoto 2023-11-15 um 16 01 13" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/1cc92098-2524-480a-baab-8b9f7fc4ba78">
<img width="443" alt="Bildschirmfoto 2023-11-15 um 16 01 24" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/fc9cc492-e571-4f39-90e3-421202d93618">

## Lineares Modell
Bilde ein lineares Modell zwischen CO2 und Zeit. Dann zeichne das mit ggplot.
```
lm_fit=lm(concentration ~ time, data = co2)
summary(lm_fit)
lines(co2$time,predict(lm_fit), col="orange", lwd = 4)
plot(co2$time, co2$concentration)
```
<img width="945" alt="image" src="https://github.com/tbilgin/InProgress/assets/26571015/a53382e7-2338-4864-9cfc-b0fa8e9b1085">

<img width="913" alt="image" src="https://github.com/tbilgin/InProgress/assets/26571015/46f97488-288b-4fb3-aade-a2ccbf3dde58">

Schauen wir mal auf die Residuen. Erinnere dich daran, dass ein Residual der Unterschied zwischen dem Wert und dem vom Modell vorhergesagten Wert für einen gegebenen Punkt ist. Ein Regressionsmodell der kleinsten Quadrate minimiert die Summe der quadrierten Residualwerte. 
```
plot(co2$time, residuals(lm_fit))
```
<img width="913" alt="image" src="https://github.com/tbilgin/InProgress/assets/26571015/03045571-09ff-4e3e-bb57-f1e001d2db3f">


## Nicht parametrisches Modell

Wir werden jetzt ein nicht parametrisches Modell probieren. Dazu braucht man zuerst eine Formel mit Werte definieren, die das Modell schätzen wird. Unsere Formel ist y~a+b*x+c*x^2, wo a, b, und c die Werte zum Schätzen sind.
```
Werte=list(a=1,b=1,c=1) 
nl_fit=nls(concentration ~ b + a * time + c * time^2,
           data = co2,
           start = Werte)
summary(nl_fit)
```
<img width="814" alt="image" src="https://github.com/tbilgin/InProgress/assets/26571015/90dfd6e6-1487-48d3-b1ea-dec08ae96f51">

```
plot(co2$time, residuals(lm_fit), col="orange")
points(co2$time, residuals(nl_fit), col="green")
```
![image](https://github.com/tbilgin/InProgress/assets/26571015/89791326-2da0-4694-98d6-0fcc253d47ae)

Die Residuen sehen viel besser aus, weil sie jetzt um 0 verteilt sind.
Und hier ist, wie man das Plot der best-Fit-Linie zeichnet.
```
plot(co2$time, co2$concentration, type = "l")
lines(co2$time,predict(lm_fit), col="orange", lwd = 4)
lines(co2$time,predict(nl_fit), col="green", lwd = 4)
```
![image](https://github.com/tbilgin/InProgress/assets/26571015/622b8dff-6aad-4a41-9d93-a35f3af39445)


## Nicht parametrisches Modell mit Sinuswellen
Schön aber man muss an die Schwankungen denken, und darüber was machen.

Also ein neues Modell:
```
Werte = list(a=1,b=1,c=1,d=1,e=1) 
sin_fit=nls(concentration ~ b+a*time+ c*time^2+d*sin(2*pi*time+e),
           data = co2,
           start = Werte)
summary(sin_fit)
```
Plots von Best-Fit-Linien
```
plot(co2$time, co2$concentration, type = "l")
lines(co2$time,predict(lm_fit), col="orange", lwd = 4)
lines(co2$time,predict(nl_fit), col="green", lwd = 4)
lines(co2$time,predict(sin_fit), col="lightblue", lwd = 4)
```
![image](https://github.com/tbilgin/InProgress/assets/26571015/0af1a571-297a-44ab-aad4-722c3ad352ef)

Plots von Residuen:
```
plot(co2$time, residuals(lm_fit), col="orange", pch = 19)
points(co2$time, residuals(nl_fit), col="green", pch = 19)
points(co2$time, residuals(sin_fit), col="lightblue", pch = 19)
```
![image](https://github.com/tbilgin/InProgress/assets/26571015/fbc0bfd0-e9cd-4eaa-9598-bf1cae05c7af)












