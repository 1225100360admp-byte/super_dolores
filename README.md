# Super Dolores — SuperApp con TDD (Flutter)

Proyecto del *Manual paso a paso con TDD* (Desarrollo Móvil Integral, UTNG).
Dominio en Dart puro, sin paquetes externos. Todo es simulación didáctica (no mueve dinero real).

## Instalación

```powershell
flutter create super_dolores
cd super_dolores
```

Luego copia sobre esa carpeta: `lib/`, `test/`, `pubspec.yaml` y `analysis_options.yaml`
(reemplaza los que trae `flutter create`) y **borra `test/widget_test.dart`**
(el que genera Flutter por defecto; si lo dejas, `flutter test` falla porque busca `MyApp`).

```powershell
flutter pub get
```

## Ciclo TDD y capturas de terminal

### 1. ROJO (captura #1)
Con `test/` y `pubspec.yaml` copiados, pero **todavía sin `lib/`** (o con `lib/` vacía):

```powershell
flutter test
```

Debe fallar (errores de importación de `package:super_dolores/...`). Toma captura.

### 2. VERDE (captura #2)
Copia `lib/` completa y corre de nuevo:

```powershell
flutter test
```

Toma captura de la terminal con el resumen final `All tests passed!`.

### 3. Verificación extra (opcional, capturas por archivo)

```powershell
flutter test test/dominio_test.dart
flutter test test/servicios_test.dart
flutter test test/retencion_test.dart
flutter test test/vms_test.dart
flutter analyze
```

### 4. Ejecutar la app

```powershell
flutter run
```

## Estructura

```
lib/
  dominio/        reglas del negocio (Dart puro)
  presentacion/
    vm/           ViewModels (inicio, monedero, chat, tienda, viajes, métricas)
    pantallas/    pantallas + mini-app de un tercero (horóscopo)
  main.dart       la "concha" (shell) de la SuperApp
test/             dominio_test, servicios_test, retencion_test, vms_test
```

## Lista de verificación del manual
- `flutter test` pasa en verde (4 archivos de pruebas).
- Mandar dinero en el chat cambia ambos saldos, deja un mensaje y avisa al destinatario.
- Una compra reparte comisión (5 %) y la suma total del dinero no cambia.
- Un viaje recorre sus estados y los saltos ilegales fallan sin tocar dinero.
- El horóscopo (tercero) no puede leer el saldo ni los chats.
- Apagar Viajes (kill switch) lo quita de la barra y bloquea sus llamadas.
- El tablero muestra DAU, WAU, MAU, stickiness y retención con la advertencia de datos sintéticos.
