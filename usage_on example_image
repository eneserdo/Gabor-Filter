import cv2
import numpy as np


def fourier2d(img):
    img2=np.fft.fft2(img)
    img2=np.fft.fftshift(img2)
    mag=np.log(abs(img2)+1)
    return abs(img2), mag


def build_filters(d, sigma, lamda, gamma):
    filters = []

    for theta in np.arange(0, np.pi, np.pi / 16):
        kern = cv2.getGaborKernel((d, d), sigma, theta, lamda, gamma, ktype=cv2.CV_32F)
        filters.append(kern)

    return filters


changing=True


def change(x):
    global changing
    changing=False


img=cv2.imread("foto\\rose.jpg", cv2.IMREAD_COLOR)

cv2.namedWindow("gabor")

cv2.resizeWindow("gabor", 700,500)
cv2.createTrackbar("d", "gabor", 100, 300, change)
cv2.createTrackbar("sigma", "gabor", 2, 15, change)
cv2.createTrackbar("theta", "gabor", 0, 180, change)
cv2.createTrackbar("lambda", "gabor", 10, 50, change)
cv2.createTrackbar("gamma*10", "gabor", 250, 500, change)


d = 100
sigma = 2
theta = 0
lamda = 10
gamma = 250


while True:

    cv2.imshow("Original",img)

    if changing==False:
        d = cv2.getTrackbarPos("d", "gabor")
        sigma = cv2.getTrackbarPos("sigma", "gabor")
        lamda = cv2.getTrackbarPos("lambda", "gabor")
        theta = cv2.getTrackbarPos("theta", "gabor")
        gamma = cv2.getTrackbarPos("gamma*10", "gabor")
        changing= True


    filters=build_filters(d, sigma, lamda, gamma/10)
    total=sum(i for i in filters)
    im2 = cv2.filter2D(img, cv2.CV_8UC3, total)
    cv2.imshow("filtered", im2)

    a=0.4
    cv2.imshow("blended", cv2.addWeighted(img,a, im2, (1-a),0))

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break


cv2.destroyAllWindows()
