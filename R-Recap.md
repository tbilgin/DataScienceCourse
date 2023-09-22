# Skripte für R-Recap

## Einführung und Entdeckung vom Dataset

Wir werden das Datai zuerst hochladen und schauen schnell, wie es aussieht: 
```
mydata = read.table("happiness", header = T)
attach(mydata)
head(mydata)
```
Welche Werte haben die Faktoren?
```
apply(mydata[,3:9], 2, mean)
```
Falls ich nur Happiness-Werte sehen möchte?
```

```
Probiere das jetzt mit anderen Faktoren.

Was sind die Dimensione, wie lang und wie breit ist das Dataset?
```

```
Wie viele Länder sind in unserem Dataset?

```

```

## Welche Faktoren spielen die grösste Rolle in Happiness?

Zuerst sehen wir mal das Figur:
```
plot(mydata)
```
Werden wir unglücklicher mit der Zeit?
```
cor.test(Happiness, Year, method = "spearman")
```
Ok, jeder berechnet einen Korrelationskoeffizient so dass wir ein Figur machen können:
```
par(mai=c(1,3,1,1))
barplot(1:6,las=1, names.arg = colnames(mydata)[4:9], horiz = T)
```



