import tkinter as tk
from tkinter import messagebox
import json
import os
class Loginr(tk.Tk):
 def __init__(self):
  super().__init__()
  self.title("MiniPime")
  self.configure(bg="medium blue") 
  self.usuarios = self.cargar_usuarios()
  self.tiendas = self.cargar_tiendas()
  self.centrar_ventana(300, 250)
  self.Inicio()
 def centrar_ventana(self, ancho, alto):
  ancho_pantalla = self.winfo_screenwidth()
  alto_pantalla = self.winfo_screenheight()
  x = (ancho_pantalla - ancho) // 2
  y = (alto_pantalla - alto) // 2
  self.geometry(f"{ancho}x{alto}+{x}+{y}")
 def cargar_usuarios(self):
  if os.path.exists("usuarios.json"):
   with open("usuarios.json", "r", encoding="utf-8") as archivo:
    try:
     data = json.load(archivo)
     return data  # Lista de diccionarios
    except json.JSONDecodeError:
     messagebox.showerror("Error", "El archivo JSON no tiene un formato válido.")
  return []
 def cargar_tiendas(self):
  if os.path.exists("tiendas.json"):
   with open("tiendas.json", "r", encoding="utf-8") as f:
    try:
     return json.load(f)
    except json.JSONDecodeError:
     return []
  return []
 def Inicio(self):
  for widget in self.winfo_children():
   widget.destroy()

  self.centrar_ventana(200, 220)

  tk.Button(self, text="Abrir tienda", bg="navy", fg="white", command=self.AbrirTienda).pack(pady=20)
  tk.Button(self, text="Crear una tienda", bg="navy", fg="white", command=self.CrearTienda).pack(pady=20)
  tk.Button(self, text="Salir", bg="crimson", fg="white", command=self.destroy).pack(pady=20)
 def CrearTienda(self):
        for widget in self.winfo_children():
            widget.destroy()

        self.centrar_ventana(200, 200)

        tk.Label(self, text="Nombre de la tienda:").pack(pady=5)
        self.entry_nueva_tienda = tk.Entry(self)
        self.entry_nueva_tienda.insert(0,"")
        self.entry_nueva_tienda.pack(pady=5)        

        tk.Label(self, text="Crear contraseña").pack(pady=5)
        self.entry_nueva_contraseña = tk.Entry(self, show="*")
        self.entry_nueva_contraseña.insert(0, "")
        self.entry_nueva_contraseña.pack(pady=5)   

        tk.Button(self, text="crear tienda", command=self.crear_tienda).pack(pady=5)  
 def crear_tienda(self):
        self.Nombre = self.entry_nueva_tienda.get()
        try:
            contraseña = self.entry_nueva_contraseña.get()
            # Asignar código único incremental
            if self.tiendas:
                ultimo_codigo = max(p["codigo"] for p in self.tiendas)
                nuevo_codigo = ultimo_codigo + 1
            else:
                nuevo_codigo = 1

            nuevo_producto = {
                "codigo": nuevo_codigo,
                "nombre": self.Nombre,
                "contraseña": contraseña
            }

            self.tiendas.append(nuevo_producto)
            self.guardar_tiendas()
            self.entry_nueva_tienda.delete(0, tk.END)
            self.entry_nueva_contraseña.delete(0, tk.END)
            self.AgregarAdmin()
        except ValueError:
            messagebox.showerror("Error", "El precio debe ser un número.")
 def AgregarAdmin(self):
        for widget in self.winfo_children():
            widget.pack_forget()

        self.centrar_ventana(400, 400)

        tk.Label(self, text="Nombre de el/la admin").pack(pady=5)
        self.entry_admin_nombre = tk.Entry(self)
        self.entry_admin_nombre.insert(0,"")
        self.entry_admin_nombre.pack(pady=5)        

        tk.Label(self, text="Edad").pack(pady=5)
        self.entry_aedad = tk.Entry(self)
        self.entry_aedad.insert(0, "")
        self.entry_aedad.pack(pady=5)

        tk.Label(self, text="Contraseña").pack(pady=5)
        self.entry_acontra = tk.Entry(self, show="*")
        self.entry_acontra.insert(0, "")
        self.entry_acontra.pack(pady=5)   

        tk.Button(self, text="Agregar admin", command=self.agregar_admin).pack(pady=5) 
 def agregar_admin(self):
        Nombre = self.Nombre
        nombre = self.entry_admin_nombre.get()
        contra = self.entry_acontra.get()
        try:
            edad = self.entry_aedad.get()
            # Asignar código único incremental
            if self.usuarios:
                ultimo_codigo = max(p["id"] for p in self.usuarios)
                nuevo_codigo = ultimo_codigo + 1
            else:
                nuevo_codigo = 1

            nuevo_vendedor = {
                "id": nuevo_codigo,
                "usuario": nombre,
                "nombre": Nombre,
                "edad": edad,
                "contraseña": contra,
                "rol": "Admin"
            }

            self.usuarios.append(nuevo_vendedor)
            self.guardar_vendedor()
            self.entry_admin_nombre.delete(0, tk.END)
            self.entry_aedad.delete(0, tk.END)
            self.Inicio()
        except ValueError:
            messagebox.showerror("Error", "El precio debe ser un número.")
 def guardar_tiendas(self):
        with open("tiendas.json", "w", encoding="utf-8") as f:
            json.dump(self.tiendas, f, indent=4)   
 def guardar_vendedor(self):
        with open("usuarios.json", "w", encoding="utf-8") as f:
            json.dump(self.usuarios, f, indent=4)
 def AbrirTienda(self):
  for widget in self.winfo_children():
   widget.destroy()
  self.centrar_ventana(200, 225)

  tk.Label(self, text="Nombre de la tienda:", bg="medium blue", fg="white").pack(pady=5)
  self.entry_tienda = tk.Entry(self)
  self.entry_tienda.insert(0,"")
  self.entry_tienda.pack(pady=5)        

  tk.Label(self, text="Contraseña", bg="medium blue", fg="white").pack(pady=5)
  self.entry_contraseña = tk.Entry(self, show="*")
  self.entry_contraseña.insert(0, "")
  self.entry_contraseña.pack(pady=5)   

  tk.Button(self, text="Abrir tienda", bg="navy", fg="white", command=self.Abrir_Tienda).pack(pady=5) 
  tk.Button(self, text="Volver", bg="crimson", fg="white", command=self.Inicio).pack(pady=5)
 def Abrir_Tienda(self): 
  usuario_ingresado = self.entry_tienda.get()
  contraseña_ingresada = self.entry_contraseña.get()

  for user in self.tiendas:
   if (
    user.get("nombre") == usuario_ingresado and
    user.get("contraseña") == contraseña_ingresada
   ):  # Oculta la ventana principal
    self.destroy()
    Login(nombre_tienda = usuario_ingresado)  # Abre la ventana del administrador
    return  # Sale de la función si encontró un usuario válido

  # Solo se muestra si ningún usuario fue válido
  messagebox.showinfo("Vendedor", "Aquí iría la ventana del vendedor (por agregar)")
class Login(tk.Tk):
 def __init__(self, nombre_tienda=None):
  super().__init__()
  self.title("Inicio de sesión")
  self.configure(bg="medium blue") 
  self.nombre_tienda = nombre_tienda
  self.usuarios = self.cargar_usuarios()
  self.centrar_ventana(300, 290)
  self.mostrar_login_unico()
 def centrar_ventana(self, ancho, alto):
  ancho_pantalla = self.winfo_screenwidth()
  alto_pantalla = self.winfo_screenheight()
  x = (ancho_pantalla - ancho) // 2
  y = (alto_pantalla - alto) // 2
  self.geometry(f"{ancho}x{alto}+{x}+{y}")
 def cargar_usuarios(self):
        if os.path.exists("usuarios.json"):
            with open("usuarios.json", "r", encoding="utf-8") as archivo:
                try:
                    data = json.load(archivo)
                    return data  # Lista de diccionarios
                except json.JSONDecodeError:
                    messagebox.showerror("Error", "El archivo JSON no tiene un formato válido.")
        return []
 def mostrar_login_unico(self):
        tk.Label(self, text="Usuario:", bg="medium blue", fg="white").grid(row=0, column=0, padx=10, pady=10, sticky="e")
        self.entry_usuario = tk.Entry(self)
        self.entry_usuario.grid(row=0, column=1, padx=10, pady=10)

        tk.Label(self, text="Contraseña:", bg="medium blue", fg="white").grid(row=1, column=0, padx=10, pady=10, sticky="e")
        self.entry_contraseña = tk.Entry(self, show="*")
        self.entry_contraseña.grid(row=1, column=1, padx=10, pady=10)

        tk.Label(self, text="Rol:", bg="medium blue", fg="white").grid(row=2, column=0, padx=10, pady=10, sticky="e")
        self.rol_var = tk.StringVar(value="Admin")
        opciones = ["Admin", "Vendedor"]
        
        self.rol_menu = tk.OptionMenu(self, self.rol_var, *opciones)
        self.rol_menu.configure(bg="navy", fg="white", highlightthickness=0, activebackground="crimson", activeforeground="white")
        self.rol_menu.grid(row=2, column=1, padx=10, pady=10)


        self.boton_login = tk.Button(self, text="Iniciar sesión",bg="navy", fg="white", command=self.verificar_credenciales)
        self.boton_login.grid(row=3, column=0, columnspan=2, pady=20)
        self.boton_login = tk.Button(self, text="Volver al inicio",bg="crimson", fg="white", command=self.VolverLoginr)
        self.boton_login.grid(row=4, column=0, columnspan=2, pady=20)
 def VolverLoginr(self):
   self.destroy()
   Loginr()
 def verificar_credenciales(self):
        usuario_ingresado = self.entry_usuario.get()
        contraseña_ingresada = self.entry_contraseña.get()
        rol_seleccionado = self.rol_var.get()
        nombre = self.nombre_tienda

        for user in self.usuarios:
            if (
                user.get("usuario") == usuario_ingresado and
                user.get("contraseña") == contraseña_ingresada and
                user.get("rol") == rol_seleccionado and
                user.get("nombre") == nombre
            ):
                messagebox.showinfo("Éxito", f"Inicio de sesión exitoso como {rol_seleccionado}.")
                self.withdraw()  # Oculta la ventana de login

                if rol_seleccionado == "Admin":
                    PrimerVAdmin(nombre_tienda=self.nombre_tienda)
                else:
                    messagebox.showinfo("Vendedor", "Aquí iría la ventana del vendedor (por agregar)")
class PrimerVAdmin(tk.Tk, tk.Toplevel):
    def __init__(self, nombre_tienda=None):
        super().__init__()
        self.title("Administrador")
        self.configure(bg="medium blue") 
        self.geometry("400x200")
        self.centrar_ventana(200, 200)
        self.nombre_tienda = nombre_tienda
        self.tiendas = self.cargar_tiendas() 
        self.usuarios = self.cargar_usuarios()
        self.productos = self.cargar_productos()
        self.VAdmin()
    def limpiar_ventana(self):
        for widget in self.winfo_children():
            widget.grid_forget()    
    def centrar_ventana(self, ancho, alto):
        ancho_pantalla = self.winfo_screenwidth()
        alto_pantalla = self.winfo_screenheight()
        x = (ancho_pantalla - ancho) // 2
        y = (alto_pantalla - alto) // 2
        self.geometry(f"{ancho}x{alto}+{x}+{y}")
    def cargar_usuarios(self):
        if os.path.exists("usuarios.json"):
            with open("usuarios.json", "r", encoding="utf-8") as archivo:
                try:
                    data = json.load(archivo)
                    return data  # Lista de diccionarios
                except json.JSONDecodeError:
                    messagebox.showerror("Error", "El archivo JSON no tiene un formato válido.")
        return []
    def cargar_productos(self):
        if os.path.exists("productos.json"):
            with open("productos.json", "r", encoding="utf-8") as archivo:
                try:
                    data = json.load(archivo)
                    return data  # Lista de diccionarios
                except json.JSONDecodeError:
                    messagebox.showerror("Error", "El archivo JSON no tiene un formato válido.")
        return []
    def VAdmin(self):
        for widget in self.winfo_children():
            widget.destroy()

        self.centrar_ventana(200, 220)

        tk.Button(self, text="Entrar a la tienda",bg="navy", fg="white", command=self.VentanaAdmin).pack(pady=20)
        tk.Button(self, text="Admnistrar vendedores",bg="navy", fg="white", command=self.AdVendedores).pack(pady=20)
        tk.Button(self, text="Eliminar tienda",bg="crimson", fg="white", command=self.eliminar_tienda).pack(pady=20)
        tk.Button(self, text="Salir",bg="crimson", fg="white", command=self.salir).pack(pady=20)
    def salir(self):
       self.destroy()
       Login()
    def salirr(self):
       self.destroy()
       Loginr()
    def AdVendedores(self):
        for widget in self.winfo_children():
            widget.destroy()

        self.centrar_ventana(400, 400)
        self.listaUsuarios = tk.Listbox(self, width=50)
        self.listaUsuarios.pack(pady=10)
        self.actualizar_listaVendedores()

        tk.Button(self, text="Agregar vendedor",bg="navy", fg="white", command=self.AgregarVendedor).pack(pady=5)
        tk.Button(self, text="Eliminar seleccionado",bg="navy", fg="white", command=self.eliminar_vendedor).pack(pady=5)
        tk.Button(self, text="Volver",bg="crimson", fg="white", command=self.VAdmin).pack(pady=5)
    def cargar_tiendas(self):
        if os.path.exists("tiendas.json"):
            with open("tiendas.json", "r", encoding="utf-8") as f:
                try:
                    return json.load(f)
                except json.JSONDecodeError:
                    return []
        return []
    def guardar_tiendas(self):
        with open("tiendas.json", "w", encoding="utf-8") as f:
            json.dump(self.tiendas, f, indent=4)
    def AgregarVendedor(self):
        for widget in self.winfo_children():
            widget.pack_forget()

        self.centrar_ventana(400, 400)

        tk.Label(self, text="Nombre de el/la vendedor/a").pack(pady=5)
        self.entry_vende_nombre = tk.Entry(self)
        self.entry_vende_nombre.insert(0,"")
        self.entry_vende_nombre.pack(pady=5)        

        tk.Label(self, text="Edad").pack(pady=5)
        self.entry_edad = tk.Entry(self)
        self.entry_edad.insert(0, "")
        self.entry_edad.pack(pady=5)

        tk.Label(self, text="Contraseña").pack(pady=5)
        self.entry_contra = tk.Entry(self, show="*")
        self.entry_contra.insert(0, "")
        self.entry_contra.pack(pady=5)   

        tk.Button(self, text="Agregar vendedor", command=self.agregar_vendedor).pack(pady=5) 
    def VentanaAdmin(self):
        for widget in self.winfo_children():
            widget.destroy()

        self.centrar_ventana(400, 500)
        self.lista = tk.Listbox(self, width=50)
        self.lista.pack(pady=10)
        self.actualizar_lista()

        tk.Label(self, text="Nombre del producto", bg="medium blue", fg="white").pack(pady=5)
        self.entry_nombre = tk.Entry(self)
        self.entry_nombre.insert(0, "")
        self.entry_nombre.pack(pady=5)

        tk.Label(self, text="Precio", bg="medium blue", fg="white").pack(pady=5)
        self.entry_precio = tk.Entry(self)
        self.entry_precio.insert(0, "")
        self.entry_precio.pack(pady=5)

        tk.Button(self, text="Agregar producto",bg="navy", fg="white", command=self.agregar_producto).pack(pady=5)
        tk.Button(self, text="Eliminar seleccionado",bg="navy", fg="white", command=self.eliminar_producto).pack(pady=5)
        tk.Button(self, text="Volver",bg="crimson", fg="white", command=self.VAdmin).pack(pady=5)
    def guardar_productos(self):
        with open("productos.json", "w", encoding="utf-8") as f:
            json.dump(self.productos, f, indent=4)
    def guardar_vendedor(self):
        with open("usuarios.json", "w", encoding="utf-8") as f:
            json.dump(self.usuarios, f, indent=4)
    def actualizar_lista(self):
        self.lista.delete(0, tk.END)
        self.lista_productos_ids = []  # Lista auxiliar para los IDs reales
        for producto in self.productos:
            if producto['nameti'] == self.nombre_tienda:
                self.lista.insert(tk.END, f"[{producto['codigo']}] {producto['nombre']} - {producto['precio']}")
                self.lista_productos_ids.append(producto['codigo'])  # Guarda el ID real
    def actualizar_listaVendedores(self):
        self.listaUsuarios.delete(0, tk.END)
        self.lista_vendedores_ids = []  # Lista auxiliar para los IDs reales
        for usuario in self.usuarios:
            if usuario['rol'] == "Vendedor" and usuario['nombre'] == self.nombre_tienda:
                self.listaUsuarios.insert(tk.END, f"[{usuario['id']}] {usuario['usuario']} - {usuario['edad']}")
                self.lista_vendedores_ids.append(usuario['id'])  # Guarda el ID real
    def agregar_producto(self):
        nombre = self.entry_nombre.get()
        try:
            precio = self.entry_precio.get()
            # Asignar código único incremental
            if self.productos:
                ultimo_codigo = max(p["codigo"] for p in self.productos)
                nuevo_codigo = ultimo_codigo + 1
            else:
                nuevo_codigo = 1

            nuevo_producto = {
                "codigo": nuevo_codigo,
                "nombre": nombre,
                "precio": precio,
                "nameti": self.nombre_tienda
            }

            self.productos.append(nuevo_producto)
            self.guardar_productos()
            self.actualizar_lista()
            self.entry_nombre.delete(0, tk.END)
            self.entry_precio.delete(0, tk.END)
        except ValueError:
            messagebox.showerror("Error", "El precio debe ser un número.")
    def agregar_vendedor(self):
        nombre = self.entry_vende_nombre.get()
        contra = self.entry_contra.get()
        try:
            edad = int(self.entry_edad.get())
            # Asignar código único incremental
            if edad >= 18:
                if self.usuarios:
                    ultimo_codigo = max(p["id"] for p in self.usuarios)
                    nuevo_codigo = ultimo_codigo + 1
                else:
                    nuevo_codigo = 1

                nuevo_vendedor = {
                    "id": nuevo_codigo,
                    "usuario": nombre,
                    "nombre": self.nombre_tienda,
                    "edad": edad,
                    "contraseña": contra,
                    "rol": "Vendedor"
                }

                self.usuarios.append(nuevo_vendedor)
                self.guardar_vendedor()
                self.actualizar_listaVendedores()
                self.entry_vende_nombre.delete(0, tk.END)
                self.entry_edad.delete(0, tk.END)
                self.AdVendedores()
            else:
                messagebox.showerror("Error", "el vendedor debe ser mayor de edad")
        except ValueError:
            messagebox.showerror("Error", "El precio debe ser un número.")
    def eliminar_producto(self):
        seleccion = self.lista.curselection()
        if seleccion:
            index = seleccion[0]
            del self.productos[index]
            self.guardar_productos()
            self.actualizar_lista()
    def eliminar_vendedor(self):
        seleccion = self.listaUsuarios.curselection()
        if seleccion:
            index_visual = seleccion[0]
            id_vendedor = self.lista_vendedores_ids[index_visual]  # Obtener el ID real

            # Buscar en self.usuarios el usuario correcto por su ID
            for i, usuario in enumerate(self.usuarios):
                if usuario['id'] == id_vendedor:
                    del self.usuarios[i]
                    break

            self.guardar_vendedor()  # Guardar la lista completa de usuarios
            self.usuarios = self.cargar_usuarios()  # 🔥 Recargar usuarios desde el JSON actualizado
            self.actualizar_listaVendedores()                    
    def eliminar_tienda(self):
        if not hasattr(self, 'nombre_tienda') or self.nombre_tienda is None:
            messagebox.showerror("Error", "No hay usuario logueado.")
            return

        # Confirmar antes de eliminar
        confirmar = messagebox.askyesno(
            "Confirmar eliminación",
            f"¿Estás seguro que quieres eliminar tu tienda '{self.nombre_tienda}'? Esta acción no se puede deshacer."
        )
    
        if not confirmar:
            return

        nombre_vendedor = self.nombre_tienda

        # Eliminar todos los productos de este vendedor
        productos_antes = len(self.productos)
        self.productos = [producto for producto in self.productos if producto['nameti'] != nombre_vendedor]
        productos_despues = len(self.productos)
        # Eliminar todos los usuarios de este vendedor
        usuarios_antes = len(self.usuarios)
        self.usuarios = [usuario for usuario in self.usuarios if usuario['nombre'] != nombre_vendedor]
        usuarios_despues = len(self.usuarios)
        # Eliminar todos la tienda de este vendedor
        self.tiendas = [tienda for tienda in self.tiendas if tienda['nombre'] != nombre_vendedor]


        self.guardar_productos()
        self.guardar_vendedor()
        self.guardar_tiendas()
        self.salirr()

        messagebox.showinfo(
            "Tienda eliminada",
            f"Se eliminaron {productos_antes - productos_despues} productos de tu tienda '{nombre_vendedor}'."
            f"Se eliminaron {usuarios_antes - usuarios_despues} usuarios de tu tienda '{nombre_vendedor}'."

        )
                   
 

if __name__ == "__main__":
    app = Loginr()
    app.mainloop()


 


