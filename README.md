# PRODIGY_AndroidDevelopment_05
import cv2
from pyzbar.pyzbar import decode
import webbrowser
# Start camera
cap = cv2.VideoCapture(0)
print("QR Code Scanner Started...")
while True:
 success, frame = cap.read()
 # Decode QR codes
 for qr in decode(frame):
 data = qr.data.decode('utf-8')
 print("Scanned Data:", data)
 # Display scanned data on screen
 pts = qr.polygon
 if len(pts) == 4:
 pts = [(pt.x, pt.y) for pt in pts]
 cv2.putText(frame, data, (50, 50),
 cv2.FONT_HERSHEY_SIMPLEX,
 0.8, (0, 255, 0), 2)
 # Open URL if QR contains link
 if data.startswith("http"):
 webbrowser.open(data)
 # Show camera window
 cv2.imshow("QR Code Scanner", frame)
 # Press Q to quit
 if cv2.waitKey(1) & 0xFF == ord('q'):
 break
cap.release()
cv2.destroyAllWindows()
