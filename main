import numpy as np
import cv2
import imutils
import datetime

gunCascade = cv2.CascadeClassifer('cascade.xml')
camera = cv2.VideoCapture(0)

firstFrame = None
gunExist = False

while True:
    ret, frame = camera.read()
    frame = imutils.resize(frame, width = 500)
    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    gun = gunCascade.detectMultiScale(gray, 1.3, 5, minSize = (100,100))
    if len(gun) > 0:
        gunExist = True
    for (x, y, w, h) in gun:
        frame = cv2.rectangle(frame, (x, y), (x + w, y + h), (255,0,0), 2)
        roiGray = gray[y:y + h, x:x + w]
        roiColor = frame[y:y + h, x:x + w]
    if firstFrame is None:
        firstFrame = gray
        continue
    cv2.putText(frame, datetime.datetime.now().strftime("% A % d % B % Y % I:% M:% S % p"), (10, frame.shape[0] - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.35, (0,0,255), 1)
    cv2.imshow("Security Feed", frame)
    key = cv2.waitKey(1) & 0xFF
    if key == ord('q'):
        break
        if gunExist:
            print("GUN Detected")
        else:
            print("guns NOT detected")

camera.release()
cv2.destroyAllWindows()