# Proyecto-Imperativa
import tkinter as tk
import tabulate
from tkinter import ttk, messagebox

# Diccionario por el momento vacío para almacenar la información del usuario después
usuario_info = {}
info_boletos = {}

def abrir_registro_usuario():
    global vcmd_numeros, usuario_info, solo_numeros
    if usuario_info:
        messagebox.showinfo("Usuario ya registrado", "Usuario ya registrado.")
        return

    ventana_registro = tk.Toplevel(principal)
    ventana_registro.title("Registro de Usuario")
    ventana_registro.geometry('600x600')
    ventana_registro.state('zoomed')

    def solo_letras(char):
        return char.isalpha() or char in "áéíóúÁÉÍÓÚ "

    def solo_numeros(char):
        return char.isdigit()

    def validar_email(email):
        dominios_permitidos = ['gmail.com', 'yahoo.com', 'outlook.com', 'hotmail.com', 'icloud.com', 'mail.com']
        dominio = email.split('@')[-1]
        return dominio in dominios_permitidos

    def guardar_y_validar():
        global usuario_info

        nombre = Enombre.get()
        apellido = Eapellido.get()
        nacionalidad = Enacionalidad.get()
        documento = Edocumento.get()
        email = Eemail.get()
        telefono = Etelefono.get()
        genero = Egenero.get()
        asistencia = Easistencia.get()
        fecha_dia = Efecha_dia.get()
        fecha_mes = Efecha_mes.get()
        fecha_anio = Efecha_anio.get()

        if not all([nombre, apellido, nacionalidad, documento, email, telefono, genero, asistencia, fecha_dia, fecha_mes, fecha_anio]):
            messagebox.showerror("Campo obligatorio", "Todos los campos son obligatorios.")
            return
        elif not validar_email(email):
            messagebox.showerror("Dominio no válido", "El dominio del correo electrónico no es válido.")
            return

        usuario_info = {
            'nombre': nombre,
            'apellido': apellido,
            'nacionalidad': nacionalidad,
            'documento': documento,
            'fecha_nacimiento': f"{fecha_dia}/{fecha_mes}/{fecha_anio}",
            'email': email,
            'telefono': telefono,
            'genero': genero,
            'asistencia': asistencia,
        }

        messagebox.showinfo("Usuario registrado correctamente", "Usuario registrado correctamente.")
        ventana_registro.destroy()

    Lnombre = tk.Label(ventana_registro, text="Primer Nombre")
    Lapellido = tk.Label(ventana_registro, text="Primer Apellido")
    Lnacionalidad = tk.Label(ventana_registro, text="Nacionalidad")
    Ldocumento = tk.Label(ventana_registro, text="Documento")
    Lfecha_nacimiento = tk.Label(ventana_registro, text="Fecha de Nacimiento")
    Lemail = tk.Label(ventana_registro, text="Email")
    Ltelefono = tk.Label(ventana_registro, text="Teléfono")
    Lgenero = tk.Label(ventana_registro, text="Género")
    Lasistencia = tk.Label(ventana_registro, text="¿Necesita asistencia? (Sí/No)")

    vcmd = (ventana_registro.register(solo_letras), '%S')
    vcmd_numeros = (ventana_registro.register(solo_numeros), '%S')

    Enombre = tk.Entry(ventana_registro, validate="key", validatecommand=vcmd)
    Eapellido = tk.Entry(ventana_registro, validate="key", validatecommand=vcmd)
    Enacionalidad = tk.Entry(ventana_registro, validate="key", validatecommand=vcmd)
    Edocumento = tk.Entry(ventana_registro, validate="key", validatecommand=vcmd_numeros)
    Eemail = tk.Entry(ventana_registro)
    Etelefono = tk.Entry(ventana_registro, validate="key", validatecommand=vcmd_numeros)
    Egenero = ttk.Combobox(ventana_registro, values=["Masculino", "Femenino", "Otro"], state='readonly')
    Easistencia = ttk.Combobox(ventana_registro, values=["Sí", "No"], state='readonly')

    # Listas de días, meses y años
    dias = [f"{i:02d}" for i in range(1, 32)]
    meses = [f"{i:02d}" for i in range(1, 13)]
    anios = [i for i in range(1900, 2025)]

    # Comboboxes para la fecha de nacimiento
    Efecha_dia = ttk.Combobox(ventana_registro, values=dias, state='readonly', width=3)
    Efecha_mes = ttk.Combobox(ventana_registro, values=meses, state='readonly', width=3)
    Efecha_anio = ttk.Combobox(ventana_registro, values=anios, state='readonly', width=5)

    Bguardar = tk.Button(ventana_registro, text="Guardar", command=guardar_y_validar)

    # Organización de los elementos
    Lnombre.place(relx=0.5, rely=0.05, anchor=tk.CENTER)
    Enombre.place(relx=0.5, rely=0.1, anchor=tk.CENTER)
    Lapellido.place(relx=0.5, rely=0.15, anchor=tk.CENTER)
    Eapellido.place(relx=0.5, rely=0.2, anchor=tk.CENTER)
    Lnacionalidad.place(relx=0.5, rely=0.25, anchor=tk.CENTER)
    Enacionalidad.place(relx=0.5, rely=0.3, anchor=tk.CENTER)
    Ldocumento.place(relx=0.5, rely=0.35, anchor=tk.CENTER)
    Edocumento.place(relx=0.5, rely=0.4, anchor=tk.CENTER)
    Lfecha_nacimiento.place(relx=0.5, rely=0.45, anchor=tk.CENTER)
    Efecha_dia.place(relx=0.43, rely=0.5, anchor=tk.CENTER)
    Efecha_mes.place(relx=0.5, rely=0.5, anchor=tk.CENTER)
    Efecha_anio.place(relx=0.57, rely=0.5, anchor=tk.CENTER)
    Lemail.place(relx=0.5, rely=0.55, anchor=tk.CENTER)
    Eemail.place(relx=0.5, rely=0.6, anchor=tk.CENTER)
    Ltelefono.place(relx=0.5, rely=0.65, anchor=tk.CENTER)
    Etelefono.place(relx=0.5, rely=0.7, anchor=tk.CENTER)
    Lgenero.place(relx=0.5, rely=0.75, anchor=tk.CENTER)
    Egenero.place(relx=0.5, rely=0.8, anchor=tk.CENTER)
    Lasistencia.place(relx=0.5, rely=0.85, anchor=tk.CENTER)
    Easistencia.place(relx=0.5, rely=0.9, anchor=tk.CENTER)
    Bguardar.place(relx=0.5, rely=0.95, anchor=tk.CENTER)

def comprar_boletos():
    global info_boletos
    if not usuario_info:
        messagebox.showerror("Usuario no registrado", "Debes registrarte antes de comprar boletos.")
    else:
        # Reemplazo de la matriz "vuelos" por la lectura del archivo
        vuelos = []
        with open("datos_vuelos.txt", "r") as file:
            # Lee cada línea del archivo
            for line in file:
                # Ignora las líneas que comiencen con #
                if not line.startswith('#'):
                    # Convierte la línea en una lista de Python
                    data = eval(line.strip())
                    vuelos.append(data)

        def continuar():
            origen = combo_origen.get()
            destino = combo_destino.get()
            fecha = combo_fecha.get()
            hora_salida = combo_hora_salida.get()
            hora_llegada = combo_hora_llegada.get()
            personas = int(Enumero_personas.get())

            if not all([origen, destino, fecha, hora_salida, hora_llegada, personas]):
                messagebox.showerror("Faltan datos", "Debes completar todos los campos.")
                return

            info_seleccionada = {
                'Origen': origen,
                'Destino': destino,
                'Fecha': fecha,
                'Hora de Salida': hora_salida,
                'Hora de Llegada': hora_llegada,
                'Número de Personas': personas
            }
            info_boletos = info_seleccionada
            ventana_pago_boletos = tk.Toplevel(principal)
            ventana_pago_boletos.title("Pago de Boletos")
            ventana_pago_boletos.geometry('600x400')
            ventana_pago_boletos.state('zoomed')

            # Código para mostrar la información seleccionada verticalmente
            for key, value in info_seleccionada.items():
                tk.Label(ventana_pago_boletos, text=f"{key}: {value}").pack(side="top", anchor="n")

            # Cuadros de información para cada tipo de vuelo
            frame_platino = ttk.LabelFrame(ventana_pago_boletos, text="Vuelo Platino")
            frame_platino.pack(pady=10, padx=10, fill="both", expand=True)

            frame_diamante = ttk.LabelFrame(ventana_pago_boletos, text="Vuelo Diamante")
            frame_diamante.pack(pady=10, padx=10, fill="both", expand=True)

            frame_premium = ttk.LabelFrame(ventana_pago_boletos, text="Vuelo Premium")
            frame_premium.pack(pady=10, padx=10, fill="both", expand=True)

            # Detalles para cada tipo de vuelo (aquí puedes agregar más widgets según sea necesario)
            ttk.Label(frame_platino, text="""- 1 artículo personal (bolso) (Debe caber debajo del asiento)
            - 1 equipaje de mano (10 kg) (Desde $195.100 COP)
            - Equipaje de bodega (23 kg) (Desde $175.600 COP)
            - Asiento Economy (Aleatoria-clasificado Aluminio)
            - Cambios de vuelo (No es permitido)
            - Reembolso (No es permitido)""").place(x=10, y=30)
            ttk.Label(frame_diamante, text="""- 1 artículo personal (bolso) (Debe caber debajo del asiento)
            - 1 equipaje de bodega (23 kg) (Debe caber en el compartimiento superior)
            - 1 equipaje de mano (10 kg) (Entrega el equipaje en el counter)
            - Asiento Economy (Filas específicas disponibles de manera aleatoria)
            - Cambios de vuelo (No es permitido)
            - Reembolso (No es permitido)""").place(x=20, y=30)
            ttk.Label(frame_premium, text="""- 1 artículo personal (bolso) (Debe caber debajo del asiento)
            - 1 equipaje de mano (10 kg) (Debe caber en el compartimiento superior)
            - 1 equipaje de bodega (23 kg) (Entrega el equipaje en el counter)
            - Asiento Plus (Sujeto a disponibilidad-clasificado Premium)
            - Cambios de vuelo (Sin cargo por cambio, antes del vuelo)
            - Reembolso (No es permitido)""").place(x=30, y=30)

            def seleccionar_vuelo(tipo_vuelo):
                info_boletos['Tipo de Vuelo'] = tipo_vuelo
                ventana_pago_exitoso = tk.Toplevel(principal)
                ventana_pago_exitoso.title("Pago Exitoso")
                ventana_pago_exitoso.geometry('400x300')
                ventana_pago_exitoso.state('zoomed')

                ttk.Label(ventana_pago_exitoso, text="¡Pago Exitoso!").pack(pady=20)
                ttk.Label(ventana_pago_exitoso, text=f"Ha seleccionado el vuelo de tipo {tipo_vuelo}.").pack()
                ttk.Label(ventana_pago_exitoso, text="¡Buen viaje!").pack(pady=20)

            Bseleccionar_platino = tk.Button(frame_platino, text="Seleccionar", command=lambda: seleccionar_vuelo("Platino")).pack()
            Bseleccionar_diamante = tk.Button(frame_diamante, text="Seleccionar", command=lambda: seleccionar_vuelo("Diamante")).pack()
            Bseleccionar_premium = tk.Button(frame_premium, text="Seleccionar", command=lambda: seleccionar_vuelo("Premium")).pack()

        # Función para actualizar los destinos disponibles basados en la selección del origen
        def actualizar_destinos(event):
            origen_seleccionado = combo_origen.get()
            destinos_disponibles = list(set([vuelo[8] for vuelo in vuelos if vuelo[7] == origen_seleccionado]))
            combo_destino['values'] = destinos_disponibles
            combo_destino.set('')

        # Función para actualizar las fechas disponibles basadas en la selección del destino
        def actualizar_fechas(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fechas_disponibles = list(set([vuelo[1] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado]))
            combo_fecha['values'] = fechas_disponibles
            combo_fecha.set('')

        # Función para actualizar las horas de salida y llegada disponibles basadas en la selección de la fecha
        def actualizar_horas(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fecha_seleccionada = combo_fecha.get()
            horas_salida_disponibles = [vuelo[2] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada]
            horas_llegada_disponibles = [vuelo[3] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada]
            combo_hora_salida['values'] = horas_salida_disponibles
            combo_hora_llegada['values'] = horas_llegada_disponibles
            combo_hora_salida.set('')
            combo_hora_llegada.set('')

        def mostrar_hora_llegada(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fecha_seleccionada = combo_fecha.get()
            hora_salida_seleccionada = combo_hora_salida.get()
            vuelo_seleccionado = [vuelo for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada and vuelo[2] == hora_salida_seleccionada]
            if vuelo_seleccionado:
                combo_hora_llegada.set(vuelo_seleccionado[0][3])
                combo_hora_llegada.configure(state='disabled')
                precio_minimo(event)
                precio_medio(event)
                precio_maximo(event)

        def precio_minimo(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fecha_seleccionada = combo_fecha.get()
            hora_salida_seleccionada = combo_hora_salida.get()
            precio_platino = [vuelo[4] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada and vuelo[2] == hora_salida_seleccionada]
            print(f"Precio Platino: {precio_platino}")  # Agregar print para debugging
            combo_precio_minimo['values'] = precio_platino
            combo_precio_minimo.set(precio_platino)
            combo_precio_minimo.configure(state='disabled')

        def precio_medio(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fecha_seleccionada = combo_fecha.get()
            hora_salida_seleccionada = combo_hora_salida.get()
            precio_diamante = [vuelo[5] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada and vuelo[2] == hora_salida_seleccionada]
            print(f"Precio Diamante: {precio_diamante}")  # Agregar print para debugging
            combo_precio_medio['values'] = precio_diamante
            combo_precio_medio.set(precio_diamante)
            combo_precio_medio.configure(state='disabled')

        def precio_maximo(event):
            origen_seleccionado = combo_origen.get()
            destino_seleccionado = combo_destino.get()
            fecha_seleccionada = combo_fecha.get()
            hora_salida_seleccionada = combo_hora_salida.get()
            precio_premium = [vuelo[6] for vuelo in vuelos if vuelo[7] == origen_seleccionado and vuelo[8] == destino_seleccionado and vuelo[1] == fecha_seleccionada and vuelo[2] == hora_salida_seleccionada]
            print(f"Precio Premium: {precio_premium}")  # Agregar print para debugging
            combo_precio_maximo['values'] =precio_premium
            combo_precio_maximo.set(precio_premium)
            combo_precio_maximo.configure(state='disabled')

        # Crear la ventana principal de selección de vuelos
        root = tk.Toplevel(principal)
        root.title("Selección de vuelos")
        root.state('zoomed')

        # Crear el frame para el menú
        frame_menu = ttk.Frame(root)
        frame_menu.pack(padx=10, pady=10)

        # Origen
        label_origen = ttk.Label(frame_menu, text="Origen:")
        label_origen.grid(row=0, column=0, padx=5, pady=5)
        opciones_origen = list(set([vuelo[7] for vuelo in vuelos]))
        combo_origen = ttk.Combobox(frame_menu, values=opciones_origen, state='readonly')
        combo_origen.grid(row=0, column=1, padx=5, pady=5)
        combo_origen.bind("<<ComboboxSelected>>", actualizar_destinos)

        # Destino
        label_destino = ttk.Label(frame_menu, text="Destino:")
        label_destino.grid(row=1, column=0, padx=5, pady=5)
        combo_destino = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_destino.grid(row=1, column=1, padx=5, pady=5)
        combo_destino.bind("<<ComboboxSelected>>", actualizar_fechas)

        # Fecha
        label_fecha = ttk.Label(frame_menu, text="Fecha:")
        label_fecha.grid(row=3, column=0, padx=5, pady=5)
        combo_fecha = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_fecha.grid(row=3, column=1, padx=5, pady=5)
        combo_fecha.bind("<<ComboboxSelected>>", actualizar_horas)

        # Hora de salida
        label_hora_salida = ttk.Label(frame_menu, text="Hora de salida:")
        label_hora_salida.grid(row=5, column=0, padx=5, pady=5)
        combo_hora_salida = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_hora_salida.grid(row=5, column=1, padx=5, pady=5)
        combo_hora_salida.bind("<<ComboboxSelected>>", mostrar_hora_llegada)

        # Hora de llegada
        label_hora_llegada = ttk.Label(frame_menu, text="Hora de llegada:")
        label_hora_llegada.grid(row=6, column=0, padx=5, pady=5)
        combo_hora_llegada = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_hora_llegada.grid(row=6, column=1, padx=5, pady=5)

        # Número de personas
        vcmd_personas = (frame_menu.register(solo_numeros), '%S')
        label_personas = ttk.Label(frame_menu, text="Número de Personas:")
        label_personas.grid(row=7, column=0, padx=5, pady=5)
        Enumero_personas = tk.Entry(frame_menu, validate="key", validatecommand=vcmd_personas)
        Enumero_personas.grid(row=7, column=1, padx=5, pady=5)

        # Precio minimo
        label_precio_minimo = ttk.Label(frame_menu, text="Precio minimo (por persona):")
        label_precio_minimo.grid(row=9, column=0, padx=5, pady=5)
        combo_precio_minimo = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_precio_minimo.grid(row=9, column=1, padx=5, pady=5)
        

        #Precio medio
        label_precio_medio = ttk.Label(frame_menu, text=" Precio medio (por persona):")
        label_precio_medio.grid(row=10, column=0, padx=5, pady=5)
        combo_precio_medio = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_precio_medio.grid(row=10, column=1, padx=5, pady=5)
        combo_precio_minimo.bind("<<ComboboxSelected>>", precio_medio)

        # Precio maximo
        label_precio_maximo = ttk.Label(frame_menu, text=" Precio maximo (por persona):")
        label_precio_maximo.grid(row=11, column=0, padx=5, pady=5)
        combo_precio_maximo = ttk.Combobox(frame_menu, values=[], state='readonly')
        combo_precio_maximo.grid(row=11, column=1, padx=5, pady=5)
        combo_precio_medio.bind("<<ComboboxSelected>>", precio_maximo)

        # Crear el botón "Continuar"
        Bcontinuar = tk.Button(frame_menu, text="Continuar", command=continuar)
        Bcontinuar.grid(row=8, column=0, columnspan=2, padx=5, pady=10)

        # Mostrar la ventana principal
        root.mainloop()

def realizar_checkin():
    if not usuario_info:
        messagebox.showerror("Usuario no registrado", "Debes registrarte antes de realizar el check-in.")
    if not info_boletos:
        messagebox.showerror("Error", "Debes de comprar un boleto antes de realizar el check-in.")
    else:
        messagebox.showinfo("Realizar Check-In", "Funcionalidad de realizar check-in próximamente.")

principal = tk.Tk()
principal.title("Agencia de vuelos JC")
principal.geometry('400x400')
principal.state('zoomed')

# Crear un título que identifique al programa
label = tk.Label(principal, text="Agencia de Vuelos JC")

# Crear y organizar los botones en la parte superior con espacios equidistantes
Bregistro_usuario = tk.Button(principal, text="Registro de Usuario", command=abrir_registro_usuario)
Bcomprar_boletos = tk.Button(principal, text="Comprar Boletos", command=comprar_boletos)
Brealizar_checkin = tk.Button(principal, text="Realizar Check-In", command=realizar_checkin)

Bregistro_usuario.grid(row=0, column=0, padx=20, pady=10)
Bcomprar_boletos.grid(row=0, column=1, padx=20, pady=10)
Brealizar_checkin.grid(row=0, column=2, padx=20, pady=10)

# Ajustar las columnas para que tengan el mismo tamaño
principal.grid_columnconfigure(0, weight=1)
principal.grid_columnconfigure(1, weight=1)
principal.grid_columnconfigure(2, weight=1)

principal.mainloop()


