import cv2
import numpy as np


def fourier2d(img):
    img2 = np.fft.fft2(img)
    img2 = np.fft.fftshift(img2)
    mag = np.log(abs(img2) + 1)
    return mag


def build_filters(d, sigma, lambda1, gamma):
    filters = []

    for theta in np.arange(0, np.pi, np.pi / 16):
        kern = cv2.getGaborKernel((d, d), sigma, theta, lambda1, gamma, ktype=cv2.CV_32F)
        filters.append(kern)

    return filters


temp = True


def change(x):
    global temp
    temp = False


img = cv2.imread("foto\\reis.jpg", cv2.IMREAD_COLOR)

cv2.namedWindow("gabor")

cv2.resizeWindow("gabor", 700, 300)
cv2.createTrackbar("d", "gabor", 400, 1000, change)
cv2.createTrackbar("sigma", "gabor", 35, 1500, change)
cv2.createTrackbar("theta", "gabor", 0, 180, change)
cv2.createTrackbar("lambda", "gabor", 3, 1500, change)
cv2.createTrackbar("gamma*100", "gabor", 150, 500, change)

d = 400
sigma = 35
theta = 0
lambda1 = 3
gamma = 150

while True:

    if temp == False:
        d = cv2.getTrackbarPos("d", "gabor")
        sigma = cv2.getTrackbarPos("sigma", "gabor")
        lambda1 = cv2.getTrackbarPos("lambda", "gabor")
        theta = cv2.getTrackbarPos("theta", "gabor")
        gamma = cv2.getTrackbarPos("gamma*100", "gabor")
        temp = True

    # For single filter

    single_gabor = cv2.getGaborKernel((d, d), sigma, theta / 180 * np.pi, lambda1, gamma / 100)
    cv2.imshow("single filter", single_gabor)
    cv2.imshow("single filter", fourier2d(single_gabor))

    # For bank of filters
    # 16 Filters with different direction (theta values)

    filters = build_filters(d, sigma, lambda1, gamma / 100)
    total = sum(i for i in filters) / 16
    cv2.imshow("bank of filter", total)
    cv2.imshow("fft of bank of filter", fourier2d(total))

    if cv2.waitKey(1) & 0xFF == ord("q"):
        break

cv2.destroyAllWindows()

#Enes Erdogan
