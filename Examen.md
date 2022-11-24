<?php
    $conn = new mysqli('localhost', 'username', 'password', 'database')
    or die ('Cannot connect to db');
    $result = $conn->query("select id, name from table");
    echo "<html>";
    echo "<body>";
    echo "<select name='id'>";
    while ($row = $result->fetch_assoc())
    {
      unset($id, $name);
      $id = $row['id'];
      $name = $row['name'];
      echo '<option value="'.$id.'">'.$name.'</option>';
    }
    echo "</select>";
    echo "</body>";
    echo
    class Estudiante
    {
    private $nombre, $grupo, $id;

    public function __construct($nombre, $grupo, $id = null)
    {
        $this->nombre = $nombre;
        $this->grupo = $grupo;
        if ($id) {
            $this->id = $id;
        }
    }

    public function crear()
    {
        global $mysql;
        $sentencia = $mysql->prepare("INSERT INTO estudiantes
            (nombre, grupo)
                VALUES
                (?, ?)");
        $sentencia->bind_param("ss", $this->nombre, $this->grupo);
        $sentencia->execute();
    }

    public static function get()
    {
        global $mysqli;
        $resultado = $mysqli->query("SELECT id, nombre, grupo FROM estudiantes");
        return $resultado->fetch_all(MYSQLI_ASSOC);
    }
    public static function getUno($id)
    {
        global $mysqli;
        $sentencia = $mysqli->prepare("SELECT id, nombre, grupo FROM estudiantes WHERE id = ?");
        $sentencia->bind_param("i", $id);
    }
    public function update()
    {
        global $mysqli;
        $sentencia = $mysqli->prepare("update estudiantes set nombre = ?, grupo = ? where id = ?");
        $sentencia->bind_param("ssi", $this->nombre, $this->grupo, $this->id);
        $sentencia->execute();
    }

    public static function delete($id)
    {
        global $mysqli;
        $sentencia = $mysqli->prepare("DELETE FROM estudiantes WHERE id = ?");
        $sentencia->bind_param("i", $id);
        $sentencia->execute();
    }
}
