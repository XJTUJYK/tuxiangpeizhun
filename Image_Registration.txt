# -*- coding: utf-8 -*-


import cv2
import numpy as np
from PIL import Image
def gen_point(event,x,y,flags,param):
    if event == cv2.EVENT_LBUTTONDBLCLK:
        print (x,y)
img1 = cv2.imread("C:\\Users\\lenovo\\Desktop\\2\\Image A.jpg")
cv2.namedWindow('image', 2)
cv2.setMouseCallback('image',gen_point)
while(1):
    cv2.imshow('image',img1)
    if cv2.waitKey(20) & 0xFF == 27:
        break
cv2.destroyAllWindows()
im = np.array(Image.open("C:\\Users\\lenovo\\Desktop\\2\\Image B.jpg"))
dsize=(3648,2736)
A = np.array([[1197,1698], [1303, 1449], [2206, 2113],[2066,1076],[1813,914],[1391,1844],[1265,1718]])
B = np.array([[910,1254],[1074,1042],[1774,1913],[1903,873],[1704,653],[1055,1445],[971,1292]])
h, s = cv2.findHomography(B, A, cv2.RANSAC)
print(h)
book = cv2.warpPerspective(im, h, dsize)
book = cv2.cvtColor(book, cv2.COLOR_RGB2BGR)
cv2.imwrite('LLL.jpg',book)







