# Program to read QR and barcode from camera and decode the data in these QR and Barcodes

# import open cv library
import cv2
from pyzbar.pyzbar import decode


# function that captures the barcodes from camera stores frames in a list then then frame by frame reads the 
# barcodes if barcode/QR code is found reads its and displays the information


def read_barcodes_from_camera():
       # Access the default camera (change the index if you have multiple cameras)
       camera = cv2.VideoCapture(0) 
     
       while True: # loop that reads and diplay the information in the barcode and QR code 
        ret, frame = camera.read()

        if not ret:
            print("Failed to access the camera.")
            break

        # Find and decode barcodes
        # list of barcodes/QR CODES 
        barcodes = decode(frame)
        

        # Display the frame
        cv2.imshow('Barcode Reader', frame)

        # Checks for barcodes / QR CODES  in the frame
        if barcodes:
            for barcode in barcodes:
                barcode_data = barcode.data.decode('utf-8')
                barcode_type = barcode.type
                print(f"Detected {barcode_type} barcode:\n{barcode_data}")
                   

        # Breaks the loop when q is pressed
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

    
    
    camera.release()
    cv2.destroyAllWindows()
    

if __name__ == "__main__":
    read_barcodes_from_camera()
