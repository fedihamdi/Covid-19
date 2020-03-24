aspect_ratio <- 4.5
plo2=ggplot(Tun, aes(Date, y=Tunidex20_Clot , colour = isConfirmed ))+
  geom_line(size = 2.5, alpha = 0.6)+
  geom_point(shape=21,size = 2)+
  theme(aspect.ratio = aspect_ratio)+
 # geom_smooth(se = FALSE)+

  scale_y_continuous(trans="log10")+
  
  labs(x = "", y = "Tunidex Value", title =  "Tunidex20 Values", subtitle = "by Confirmed Cases")+
  geom_text(aes(label = Tunidex_Clot), nudge_y = 0.006, color = "blue", size = 1.1)+
  scale_colour_brewer(palette = "Set2")+
  theme_fivethirtyeight()+
  theme(legend.position="bottom", legend.direction="horizontal", legend.title = element_blank(), axis.text = element_text(size = 14),
        legend.text = element_text(size = 13), axis.title = element_text(size = 14), axis.line = element_line(size = 0.4, colour = "grey10"),
        plot.background = element_rect(fill = "#EFEFEF"), legend.background = element_rect(fill = "#DCDCDC"))
ggsave(plo2, height = 7 , width =  aspect_ratio)
#######
library(gganimate)
#######
gp=plo2 + geom_point() + transition_reveal(Date)

anim_save("outplot.gif",animate(gp, height = 500, width =650))
