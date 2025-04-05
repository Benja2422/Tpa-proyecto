
import tkinter as tk
from tkinter import messagebox
import os
import json

class Login(tk.Tk):
 def __init__(self):
  super().__init__()
  self.title("Inicio de sesión")
  self.usuarios = self.cargar_usuarios()
  self.mostrar_tipo_usuario()
  self.centrar_ventana(345, 280)
 
 def centrar_ventana(self, ancho, alto):
  ancho_pantalla = self.winfo_screenwidth()
  alto_pantalla = self.winfo_screenheight()
  x = (ancho_pantalla - ancho) //2
  y = (alto_pantalla - alto) //2
  self.geometry(f"{ancho}x{alto}+{x}+{y}")

 def cargar_usuarios(self):
  if os.path.exists("usuarios.json"):
   with open("usuarios.json", "r") as archivo:
    return json.load(archivo)
  return
 
 def guardar_usuarios(self):
  with open("usuario.json", "w") as archivo:
   json.dump(self.usuarios, archivo, indent=4)

 def limpiar_ventana(self):
  for widget in self.winfo_children():
   widget.grid_forget()

 def mostrar_tipo_usuario(self):
  self.limpiar_ventana()
  self.grid_columnconfigure(0, weight=1)
  self.grid_columnconfigure(1, weight=1)
  self.label_opcion = tk.Label(self, text= "Cargo")
  self.label_opcion.grid(row=0, column=0, columnspan=3, pady=10, sticky="NSEW")
  self.boton_admin = tk.Button(self, text= "Administrador", command=self.InCe_admin)
  self.boton_admin.grid(row=1, column=0, columnspan=3, pady=10, sticky="NSEW")
  self.boton_vendedor = tk.Button(self, text= "Vendedor", command=self.InCe_vend)
  self.boton_vendedor.grid(row=2, column=0, columnspan=3, pady=10, sticky="NSEW")

 def InCe_admin(self):
  self.limpiar_ventana()
  self.label_admin = tk.Label(self, text= "Administrador")
  self.label_admin.grid(row=0, column=0, padx=10, pady=10)
  self.entry_admin = tk.Entry(self)
  self.entry_admin.grid(row=0, column=1, padx=10, pady=10)
  self.label_contraseña = tk.Label(self, text= "Contraseña")
  self.label_contraseña.grid(row=1, column=0, padx=10, pady=10)
  self.entry_contraseña = tk.Entry(self, show= "*")
  self.entry_contraseña.grid(row=1, column=1, padx=10, pady=10)
  self.boton_InCe = tk.Button(self, text= "Iniciar sesión", command=self.ver_cr_admin)
  self.boton_InCe.grid(row=2, column=0, columnspan=2, pady=10)
  self.boton_volver = tk.Button(self, text= "Volver", command=self.mostrar_tipo_usuario)
  self.boton_volver.grid(row=4, column=0, columnspan=2, pady=10)

 def ver_cr_admin(self):
  admin_usuario = "admin"
  admin_contrasena = "admin123" 
  admin = self.entry_admin.get()
  contraseña = self.entry_contraseña.get()

  if admin in admin_usuario and contraseña == admin_contrasena:
   self.destroy()
   #Ventanaadmin()
  else:
   messagebox.showerror("Usuario o contraseña incorrecto")

 def InCe_vend(self):
  self.limpiar_ventana()
  self.label_admin = tk.Label(self, text= "Vendedor")
  self.label_admin.grid(row=0, column=0, padx=10, pady=10)
  self.entry_admin = tk.Entry(self)
  self.entry_admin.grid(row=0, column=1, padx=10, pady=10)
  self.label_contraseña = tk.Label(self, text= "Contraseña")
  self.label_contraseña.grid(row=1, column=0, padx=10, pady=10)
  self.entry_contraseña = tk.Entry(self, show= "*")
  self.entry_contraseña.grid(row=1, column=1, padx=10, pady=10)
  self.boton_InCe = tk.Button(self, text= "Iniciar sesión", command=self.ver_cr_vende)
  self.boton_InCe.grid(row=2, column=0, columnspan=2, pady=10)
  self.boton_volver = tk.Button(self, text= "Volver", command=self.mostrar_tipo_usuario)
  self.boton_volver.grid(row=4, column=0, columnspan=2, pady=10)

 def ver_cr_vende(self):
  vende = self.entry_admin.get()
  contraseña_vende = self.entry_contraseña.get()

  if vende in self.usuarios and self.usuarios[vende] == contraseña_vende:
   self.destroy()
   #Tienda_vendedor()
  else:
   messagebox.showerror("Usuario o contraseña incorrecto")


if __name__ == "__main__":
 app = Login()
 app.mainloop()
