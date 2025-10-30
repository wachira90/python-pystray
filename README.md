# python pystray

## Using pystray (simple and cross-platform)

```py
pip install pystray Pillow
```


```py
import pystray
from PIL import Image

# Define functions for your menu actions
def show_window(icon, item):
    """Simulate showing a window by printing a message."""
    print("Showing the main window...")

def quit_app(icon, item):
    """Quit the application."""
    icon.stop()

# Create a simple icon image (a red square)
width, height = 64, 64
image = Image.new('RGB', (width, height), 'red')

# Create the menu
menu = pystray.Menu(
    pystray.MenuItem('Show', show_window),
    pystray.MenuItem('Quit', quit_app)
)

# Create and run the tray icon
icon = pystray.Icon('test_app', image, 'My Tray App', menu)
icon.run()
```

## Using PyQt (advanced GUI framework)

```sh
pip install PyQt6
```


```py
import sys
from PyQt6.QtGui import QIcon, QAction
from PyQt6.QtWidgets import QApplication, QSystemTrayIcon, QMenu, QMainWindow, QLabel

class TrayApp(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("System Tray App")
        self.setGeometry(300, 300, 300, 200)
        self.setWindowIcon(QIcon("icon.png"))
        
        self.label = QLabel("Hello from the main window!", self)
        self.setCentralWidget(self.label)

        self.tray = QSystemTrayIcon(self)
        self.tray.setIcon(QIcon("icon.png"))

        menu = QMenu()
        show_action = QAction("Show", self)
        quit_action = QAction("Quit", self)
        
        show_action.triggered.connect(self.show)
        quit_action.triggered.connect(QApplication.instance().quit)

        menu.addAction(show_action)
        menu.addAction(quit_action)
        self.tray.setContextMenu(menu)

        self.tray.activated.connect(self.handle_tray_click)
        self.tray.show()

    def handle_tray_click(self, reason):
        if reason == QSystemTrayIcon.ActivationReason.Trigger:
            self.show()

if __name__ == '__main__':
    app = QApplication(sys.argv)
    app.setQuitOnLastWindowClosed(False)
    
    window = TrayApp()
    window.show()
    sys.exit(app.exec())
```

