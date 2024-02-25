#import libraries
import cv2
import matplotlib.pyplot as plt
import numpy as np

path='dir' % image directory path
filename='Dumbo.jpg'
img=cv2.imread(path+'/'+filename)
gray_img=cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)

#convert image into 3 regions with r,g,b patches
#red mask
h_red=int(gray_img.shape[0])
w_red=int(gray_img.shape[1]/3)
red_mask=np.zeros((h_red,w_red,3))
red_mask[:,:,2]=gray_img[0:h_red,0:w_red]

#green mask
h_green=h_red
w_green=w_red
green_mask=np.zeros((h_green,w_green,3))
green_mask[:,:,1]=gray_img[0:h_green,w_red:w_red+w_green]

#blue mask
h_blue=h_red
w_blue=w_red
blue_mask=np.zeros((h_blue,w_blue,3))
blue_mask[:,:,0]=gray_img[0:h_blue,w_green+w_red:]

img[:,0:w_red,:]=blue_mask
# img[:,w_red:w_red+w_green,:]=green_mask # Can color the middle patch as well
img[:,w_red+w_green:,:]=red_mask

