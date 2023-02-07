Validation of invasion demo
[From](https://github.com/Almo96/Paramutations_TEs/blob/main/Validation/2022_08_01_Validation_1_invasion.md)

Introduction
With this validation we wanted to prove that the simulator will generate on average the number of insertions predicted by the equation:

c_{t}=c_{0}(1+\mu)^t

c_{t} TE copies at generation t

c_{0} TE copies at generation 0

\mu Transposition rate

t Generation

Initial conditions:
c_{0}=10

\mu = 0.1

t=100.


A chromosome of size 1Mb and no piRNA clusters. We used 500 replicates


  library(ggplot2)
  library(RColorBrewer)
  library(plyr)
  library(gridExtra)
  theme_set(theme_bw())

  cn<-seq(0,99,1)
  res<-10*1.1^cn
  theo<-data.frame(x=1:100,y=res)
  validation<-read.table("2023_02_05_Validation_1_invasion", fill = TRUE, sep = "\t")
  names(validation)<-c("rep", "gen", "popstat", "spacer_1", "fwte", "avw", "minw","avtes", "avpopfreq", "fixed", "spacer_2", "phase", "fwcli","avcli","fixcli","spacer_4","avbias","3tot", "3cluster")

  gl<-ggplot()+geom_line(data=validation,aes(x=gen,group=rep,y=avtes*1000),alpha=0.15,size=0.3)+scale_y_log10()+geom_line(data=theo,aes(x=x,y=y),size=2)+theme(legend.position="none")+ylab("TE copies in the population")+xlab("generation")
  plot(gl)
  
  
 
