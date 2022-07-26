# README

## Codigos de CONSOLA!

Cree un nuevo proyecto usando el comando rails new proyecto_inicio_sesion.
-> rails new proyecto_inicio_sesion

Cree un nuevo modelo llamado 'Usuario' con la información anterior.
-> rails g model User first_name:string last_name:string email_address:string age:integer
-> rails db:migrate

Rails inmediatamente creará el campo ID como clave primaria, que se incrementa automáticamente 
así como las marcas de tiempo created_at  y  updated_at.

Cree algunos registros en la tabla usuarios utilizando la consola de Rails.

-> User.create(first_name:"Cristian", last_name:"Uribe", email_address:"eprcristian@gmail.com", age:"36")

Ahora, agregue algunas validaciones al modelo para que:
Requiera los cuatro campos.
La edad tiene que ser numérica.
El nombre y el apellido deben tener una longitud mínima de 2 caracteres cada uno.
La edad tiene que estar entre 10 y 150 (consulte http://apidock.com/rails/ActiveModel/Validations/HelperMethods/validates_numericality_of para obtener ayuda)
Estás familiarizado con .save  y  .valid?
Utilice .errors  y  .errors.full_messages para que pueda ver o mostrar los mensajes de error cuando fallen las validaciones.
Usando la consola de Rails...

class User < ApplicationRecord
    validates :first_name, presence: true, length: { minimum: 2, too_short: ':Nombre debe tener minimo 2 caracteres' } 
    validates :last_name, presence: true, length: { minimum: 2, too_short: ':Nombre debe tener minimo 2 caracteres' }
    validates :email_address, presence: true
    validates :age, presence: true, numericality: { greater_than: 10, less_than: 150, message: 'Please enter a valid age' }
end

Verifique si le permite ingresar algunos registro que no cumplan con las reglas de validación que establecimos 
(ej. trate de crear un registro don la edad sea 5 ó mayor a 150 ó donde el nombre sea solo 1 caracter, etc.).

Asegúrate que tu consola devuelva los mensaje de error apropiados cuando intentas guardar un registro que no cumple 
con las reglas de validación.

-> User.create(first_name:"Cristian", last_name:"Uribe", email_address:"eprcristian@gmail.com", age:36).valid?
true

-> User.create!(first_name:"C", last_name:"U", email_address:"eprcristian@gmail.com", age:"6")
   (56.7ms)  SELECT sqlite_version(*)
C:/Ruby31-x64/lib/ruby/gems/3.1.0/gems/activerecord-6.1.6/lib/active_record/validations.rb:80:in `raise_validation_error': 
Validation failed: First name :Nombre debe tener minimo 2 caracteres, Last name :Nombre debe tener minimo 2 caracteres, Age Please enter a valid age (ActiveRecord::RecordInvalid)

Consultar todos los usuarios.
-> User.all

Consultar el primer usuario.
-> User.first

Consultar el último usuario.
-> User.last

Consultar todos los usuarios ordenados por el primer nombre (consulte las reglas para ordenar y más en  http://guides.rubyonrails.org/active_record_querying.html#ordering)
-> User.order(:first_name)

Consultar el registro de usuario cuyo id es 3 y cambiar el apellido por otro valor. Haz esto directamente en la consola utilizando .find  y  .save.
-> u = User.find(3)

-> u.last_name = "cambio"

-> u.save

Elimine el registro de usuario cuyo id es 4 (utilice algo como Usuario.find(2).destroy...).
-> User.find(4).destroy


