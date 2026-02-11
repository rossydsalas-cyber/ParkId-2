```mermaid
classDiagram
    class Usuario {
        -string nombre
        -string apellido
        -string numeroDocumento
        -string nombreEmpresa
        +validarAccesoCedula()
        +solicitarMembresia()
    }

    class Administrador {
        +gestionarRegistro()
        +generarReportes()
        +generarBloqueo()
    }

    class Vehiculo {
        -string placa
        -string categoriaVehiculo
        -Puesto puestoAsignado
        +vincularPuesto(Puesto p)
    }

    class Puesto {
        -string codigoPuesto
        -string zona
        -string estadoPuesto
        +actualizarEstado()
    }

    class RegistroAcceso {
        -datetime fechaEntrada
        -datetime fechaSalida
        -string documentoValidado
        +registrarMovimiento()
    }

    class Membresia {
        -string nombrePlan
        -decimal costo
        -date fechaVencimiento
        -string estado
        +verificarVigencia()
    }

    class Pago {
        #string metodo
        #decimal monto
        +procesarPago()
    }

    %% RELACIONES ACTUALIZADAS
    Usuario <|-- Administrador : es_un
    Usuario "1" -- "*" Vehiculo : posee
    Usuario "1" o-- "1" Membresia : adquiere
    
    %% UNIÓN TOTAL: Composición (El puesto es parte del Vehículo)
    Vehiculo "1" *-- "1" Puesto : objeto_asignado
    
    %% FLUJO OPERATIVO
    Usuario ..> RegistroAcceso : valida_con_cedula
    RegistroAcceso ..> Vehiculo : verifica_parqueo
    Membresia ..> Pago : genera
    ```