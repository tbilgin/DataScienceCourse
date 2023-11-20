# Logistische Regression
```
install.packages("mlbench")
data("PimaIndiansDiabetes2", package = "mlbench")
```

```
head(PimaIndiansDiabetes2)
glimpse(PimaIndiansDiabetes2)
```
```
apply(PimaIndiansDiabetes2[,1:8], 2, shapiro.test)
```
```
diabetes.data <- na.omit(PimaIndiansDiabetes2)
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  head()
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  glimpse()
```

```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(glucose, prob)) +
  geom_point(alpha = 0.2)
```
```
model <- glm( diabetes ~., data = diabetes.data, family = binomial)
summary(model)
```
```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(glucose, prob)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "binomial")) +
  labs(
    x = "Glukose",
    y = "Diabetes"
  )
```
```
exp(summary(model)$coeff[,1])
```

# Hausaufgabe: Darstellung der Regressionen

Wir haben im Unterricht die Regression für Glukose gezeichnet. Jetzt bitte zeichne die Plots auch für die Körper-Gewicht Index und Familiengeschichte und antworte die folgenden Fragen:
- Wie anders sehen die Graphs aus?
- Wo siehst du die Gewichte der Punkte?
- Wie sind die Kurven? Welche sind steiler?
- Wie gross sind die Abweichungen?
- Jetzt vergleiche die p-Werte und Odds Ratio (Quotenverhältnis) für diese drei Variable.
Wir werden diese im Unterricht diskutieren.

```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(mass, prob)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "binomial")) +
  labs(
    x = "Körper-Gewicht-Index",
    y = "Diabetes"
  )
```
<img width="510" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/7a687b93-838c-47ac-b692-c698d9c67ccd">

```
diabetes.data %>%
  mutate(prob = ifelse(diabetes == "pos", 1, 0)) %>%
  ggplot(aes(pedigree, prob)) +
  geom_point(alpha = 0.2) +
  geom_smooth(method = "glm", method.args = list(family = "binomial")) +
  labs(
    x = "Familiengeschichte",
    y = "Diabetes"
  )
```
<img width="516" alt="image" src="https://github.com/tbilgin/DataScienceCourse/assets/26571015/af7bb53d-1210-42d2-82dd-ebf4af8ffcb7">






