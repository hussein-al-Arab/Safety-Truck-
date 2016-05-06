# Safety-Truck-

import RPi.GPIO as GPIO
import picamera
import time

from picamera import PiCamera
from time import sleep

GPIO.setwarnings(False)
GPIO.setmode(GPIO.BOARD)
GPIO.setup(3, GPIO.IN)
GPIO.setup(10, GPIO.OUT)
GPIO.setup(8, GPIO.IN)
GPIO.setup(5, GPIO.OUT)

camera= PiCamera()
while True:
    while GPIO.input(3)==1:
        camera.start_preview()
        sleep(3)
    while GPIO.input(3)==0:
        camera.stop_preview()
        sleep(0.5)        
    GPIO.output(10, False)
    time.sleep(1)
    GPIO.output(10, True)
    time.sleep(1)
    GPIO.output(10, False)

    while GPIO.input(8)==0:
            signalOff=time.time()

    while GPIO.input(8)==1:
            signalOn=time.time()

    timePassed=signalOn-signalOff
    distance=timePassed*171.50
    if distance <1:
        GPIO.output(5, True)
