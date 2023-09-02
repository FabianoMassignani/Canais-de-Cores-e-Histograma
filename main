import sys
from PyQt5.QtWidgets import (
    QApplication,
    QMainWindow,
    QWidget,
    QVBoxLayout,
    QPushButton,
    QLabel,
    QFileDialog,
)
import os

import matplotlib.pyplot as plt
import cv2


class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.selected_image = None
         
        self.setWindowTitle("Conversor de Espaços de Cores")
        self.setGeometry(100, 100, 400, 300)

        layout = QVBoxLayout()

        self.select_button = QPushButton("Selecionar Imagem")
        self.select_button.clicked.connect(self.open_image)
        layout.addWidget(self.select_button)

        self.select_button1 = QPushButton("RGB -> GRAY")
        self.select_button1.clicked.connect(self.process_image_1)
        layout.addWidget(self.select_button1)
        self.select_button1.setDisabled(True)
  
        self.select_button2 = QPushButton("RGB -> XYZ")
        self.select_button2.clicked.connect(self.process_image_2)
        layout.addWidget(self.select_button2)
        self.select_button2.setDisabled(True)
        
        self.select_button3 = QPushButton("RGB -> YCrCb")
        self.select_button3.clicked.connect(self.process_image_3)
        layout.addWidget(self.select_button3)
        self.select_button3.setDisabled(True)
        
        self.select_button4 = QPushButton("RGB -> HSV")
        self.select_button4.clicked.connect(self.process_image_4)
        layout.addWidget(self.select_button4)
        self.select_button4.setDisabled(True)
        
        self.select_button5 = QPushButton("RGB -> HLS")
        self.select_button5.clicked.connect(self.process_image_5)
        layout.addWidget(self.select_button5)
        self.select_button5.setDisabled(True)        
        
        self.select_button6 = QPushButton("RGB -> CIE L*a*b*")
        self.select_button6.clicked.connect(self.process_image_6)
        layout.addWidget(self.select_button6)
        self.select_button6.setDisabled(True)
                
        self.select_button7 = QPushButton("RGB -> CIE L*u*v*")
        self.select_button7.clicked.connect(self.process_image_7)
        layout.addWidget(self.select_button7)
        self.select_button7.setDisabled(True)
        
        self.central_widget = QWidget()
        self.central_widget.setLayout(layout)
        self.setCentralWidget(self.central_widget)

    def process_image_1(self):
        gray_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2GRAY)
        self.show_image("GRAY", gray_image, False)
       
    
    def process_image_2(self):
        xyz_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2XYZ)
        self.show_image("XYZ", xyz_image, True)
         
            
    def process_image_3(self):
        ycrcb_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2YCrCb)
        self.show_image("YCrCb", ycrcb_image,True)
     
            
    def process_image_4(self):
        hsv_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2HSV)
        self.show_image("HSV", hsv_image ,True) 
   
            
    def process_image_5(self):
        hls_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2HLS)
        self.show_image("HLS", hls_image ,True)
         
            
    def process_image_6(self):
        lab_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2Lab)
        self.show_image("CIE L*a*b*", lab_image ,True )
           
                    
    def process_image_7(self):
        luv_image = cv2.cvtColor(self.selected_image, cv2.COLOR_BGR2Luv)
        self.show_image("CIE L*u*v*", luv_image ,True)
      
    def show_image(self, name, image, use_hsv_split=False):
        if use_hsv_split:
            h, s, v = cv2.split(image)
            cv2.imshow('Channel h', h)
            cv2.imshow('Channel s', s)
            cv2.imshow('Channel v', v)
    
            self.save_histogram(h, "Hue_Histogram")
            self.save_histogram(s, "Saturation_Histogram")
            self.save_histogram(v, "Value_Histogram")
            self.plot_normalized_histogram(image)
        else:
            self.plot_normalized_histogram_gray(image)
            
        self.save_histogram(image, name)   
        cv2.imshow(name, image)
         
    def plot_normalized_histogram(self, image):
        colors = ('b', 'g', 'r')

        for i, color in enumerate(colors):
            hist = cv2.calcHist([image], [i], None, [256], [0, 256])
            cv2.normalize(hist, hist, 0, 1, cv2.NORM_MINMAX)  # Normaliza o histograma
            plt.plot(hist, color=color)
        
        plt.title('Normalized Image Histogram')
        plt.xlabel('Pixel Value')
        plt.ylabel('Normalized Frequency')
        plt.legend(['Blue Channel', 'Green Channel', 'Red Channel'])
        plt.show()
        
    def plot_normalized_histogram_gray(self, image):
       
        hist = cv2.calcHist([image], [0], None, [256], [0, 256])
        cv2.normalize(hist, hist, 0, 1, cv2.NORM_MINMAX)  # Normaliza o histograma
        plt.plot(hist, color='gray')
        
        plt.title('Normalized Image Histogram')
        plt.xlabel('Pixel Value')
        plt.ylabel('Normalized Frequency')
        plt.legend(['Gray Channel'])
        plt.show()
 
                
    def save_histogram(self, image, title):
        script_directory = os.path.dirname(os.path.abspath(__file__))
        output_filename = os.path.join(script_directory, f"{title}.png")
        cv2.imwrite(output_filename, image)
        print(f"Imagem processada salva como '{output_filename}'.")   
        
    def open_image(self):
        options = QFileDialog.Options()
        options |= QFileDialog.ReadOnly

        image_path, _ = QFileDialog.getOpenFileName(self, "Selecionar Imagem", "", "Imagens (*.png *.jpg *.bmp *.gif);;Todos os Arquivos (*)", options=options)

        if image_path:
            try:
                self.selected_image = cv2.imread(image_path)
                if self.selected_image is not None:
                    cv2.imshow("RGB", self.selected_image)

                    for button in [self.select_button1, self.select_button2, self.select_button3, self.select_button4, self.select_button5, self.select_button6, self.select_button7]:
                        button.setDisabled(False)

                    cv2.waitKey(0)
                else:
                    print("Erro ao carregar a imagem.")
            except Exception as e:
                print("Erro ao abrir a imagem:", str(e))
        else:
            print("Nenhuma imagem selecionada.")

    #   def show_hsv_equalized(image):
    #     H, S, V = cv2.split(cv2.cvtColor(image, cv2.COLOR_BGR2HSV))
    #     eq_V = cv2.equalizeHist(V)
    #     eq_image = cv2.cvtColor(cv2.merge([H, S, eq_V]), cv2.COLOR_HSV2RGB)
    #     plt.imshow(eq_image)
    #     plt.show()

if __name__ == "__main__":
    app = QApplication(sys.argv)
    main_window = MainWindow()
    main_window.show()
    sys.exit(app.exec_())
