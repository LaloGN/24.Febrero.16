# 24.Febrero.16
### Ejercio Lalo ###
### Importar la base de datos .dbf en R
require(foreign)
coe1t215<-read.dbf("C:\\Users\\SALA-C2\\Downloads\\COE1T215.dbf")

### Seleccionar al Estado de México
mex<-subset(coe1t215,ENT=="15") 
attach(mex)

### Etiquetar las preguntas ¿Aproximadamente cuántas personas, incluyendo al dueño, laboran donde trabaja ...?p3
mex$P3L<-ordered(mex$P3L,levels=c("01","02","03","04","05","06","07","08","09","10","11","99"),
labels=c("1 persona","2 a 5 personas","6 a 10 personas","11 a 15 personas","16 a 20 personas","21 a 30 personas",
"31 a 50 personas","51 a 100 personas","101 a 250 personas","251 a 500 personas","501 y más personas","No sabe"))

### P5
mex$P5<-ordered(mex$P5,levels=c("1","2","3","9"),labels=c("Sí","No trabajó la semana pasada",
"No se encontró en esa situación","No sabe"))
mex$P2E<-ordered(mex$P2E,levels=c("1","2","3","4","5","6","9"),
labels=c("una persona temporalemte ausente de su actividad u oficio?",
"pensionado o jubilado de su empleo?","estudiante?","una persona que se dedica a los quehaceres de su",
"una persona con alguna limitación fisica o mental que le impide trabajar el resto de su vida?","Otra condición",
"No sabe"))
View(mex)
  
### P1=sexo 
tabla1<-table(mex$P3L,mex$P1)
View(tabla1)
tabla2<-table(mex$P5,mex$P1)
View(tabla2)
tabla3<-table(mex$P2E,mex$P1)
View(tabla3)


install.packages("questionr")
library(questionr)
tablaexp1<-wtd.table(mex$P3L,edomex$P1,weights=FAC)
tablaexp1<-wtd.table(mex$P5,edomex$P1,weights=FAC)
tablaexp1<-wtd.table(mex$P2E,edomex$P1,weights=FAC)
