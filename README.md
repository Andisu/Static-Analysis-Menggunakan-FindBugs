# Static-Analysis-Menggunakan-FindBugs

Diperlukan findbugs-3.0.0, apache-ant-1.9.4 dan jdk1.8.0_20
Di simpan di localdisk C apache-ant-1.9.4 dan findbugs-3.0.0 dan  jdk1.8.0_20 di folder Program Files/Java 

Struktur Direktori dan Berbagai File
Nama Folder Utama : modul7

.
|-- build.xml
|-- classes
`-- src
|-`-- vehicles
|---`-- Bicycle.java
|---`-- BicycleMain.java

Penjelasan Dari Struktur direktori di atas

Dari folder utama adalah modul7 dan di dalam modul7 ada 2 folder yaitu classes dan src dan 1 file build.xml, di dalam folder src ada 1 folder yaitu vehicles dan di dalam folder vehicles ada 2 file java yaitu BicycleMain.java dan Bicycle.java dan folder classes tidak ada isinya.
Membuat Folder di Direktori di Local di C dengan nama modul7 dengan mengikuti perintah Struktur Direktori di atas Dan Membagi file-file yang ada ke masing-masing direktori atau folder.

Isi dari file build.xml
<project name="findbugs" default="findbugs" basedir=".">//Nama project
<property name="classes.dir" value="classes" />//direktori classes value ya classes
<property name="src.dir" value="src" />//direktori src value ya src
<path id="cpath">//pembuka  id cpath
<pathelement location="${classes.dir}"/>//lokasinya
</path> //penutup id path
<target name="clean">//target namanya clean
<echo message="Cleaning and creating new directory" />//isi Massage
<delete dir="${classes.dir}" />//menghapus dir di classes
<mkdir dir="${classes.dir}" />//membuat di dir
</target>//penutup target dengan nama clean
<target name="compile" depends="clean">//melakukan cleaning di dir classes
<echo message="compiling all vehicles and tests classes" />//isi Massage
<javac debug="true"
source="1.5" classpathref="cpath"
srcdir="${src.dir}" destdir="${classes.dir}"/>//javac ya true, source 1.5 classya cpath di direktori src dan direktori classes
</target>//penutup target namanya compile
<target name="run" depends="compile">//target namanya run
<java classname="vehicles.BicycleMain" classpathref="cpath"/>//dir vehicles 
</target>//penutup target namanya run
<property name="findbugs.home" value="C:\findbugs-3.0.0" />//lokasi findbugs
<taskdef name="findbugs" classname="edu.umd.cs.findbugs.anttask.FindBugsTask">//nama class
<classpath>//pembuka target class
<pathelement location="${findbugs.home}/lib/findbugs.jar" />//lokasi di dir lib yang isinya findbugs.jar

<pathelement location="${findbugs.home}/lib/findbugs-ant.jar" />//lokasi di dir lib yang isinya findbugs-ant.jar
</classpath>//penutup classpath
</taskdef>//penutup taskdef
<target name="findbugs" depends="compile">//mengcompile seluruh data

<findbugs home="${findbugs.home}"
output="text"
outputFile="findbugs-results.txt" >//output
<sourcePath path="${src.dir}" />//dir src
<class location="${classes.dir}" />//lokasi di dir classes
</findbugs>//penutup findbugs
Isi dari file Bicycle.java
package vehicles; //nama package  “vehicles”
public class Bicycle {  //nama class “Bicycle”

public int cadence; //variabel cadence menggunakan type data integer
public int gear; //variabel gear menggunakan type data integer
public int speed; //variabel speed menggunakan type data integer

public Bicycle(int startCadence, int startSpeed, int startGear) { //variabel menggunakan type data integer
gear = startGear;  //variabel gear sama dengan variabel startGear
cadence = startCadence; //variabel cadence sama dengan variabel startCadence
speed = startSpeed; //variabel speed sama dengan variabel startSpeed
}

public void setCadence(int newValue) {  { //class setGadence variabel newValue menggunakan type data integer
cadence = newValue; //class cadence variabel sama dengan  newValue 
}
public void setGear(int newValue) { //class setGear variabel newValue menggunakan type data integer
gear = newValue; class gear variabel sama dengan  newValue
}
public void setSpeed(int newValue) { //class setSpeed  variabel newValue menggunakan type data integer
speed = newValue; class speed  variabel sama dengan  newValue
}
public int getGear() {
return gear; //cetak hasil gear
}
public int getCadence() {
return cadence; //cetak hasil cadence
}
public int getSpeed() {
return speed; //cetak hasil speed
}
public void applyBrake(int decrement) {
speed -= decrement; //speed berkurang
}
public void speedUp(int increment) {
speed += increment; //speed bertambah
}
}
Isi dari file BicycleMain.java 
package vehicles; //nama package  “vehicles”
import vehicles.*; //masukkan   “vehicles”
public class BicycleMain {//nama class  “BicycleMain”
public static void main (String args[]) {
Bicycle Bike = new Bicycle(10, 20, 1); //Membuat Variabel Bike = Bicycle 
System.out.println("We have a new bicycle wth speed = " + Bike.getSpeed() + ", cadence = " + Bike.getCadence() + ", gear = " + Bike.getGear());
} //output speed,cadence dan gear 
}
Setting di Command Prompt (Setting findbugs, ant_home, java_home dan path)
Buka Command Prompt
Ketikan :
set ANT_HOME=C:\apache-ant-1.9.4
set JAVA_HOME=C:\Program Files\Java\jdk1.8.0_20
set FINDBUGS_HOME=C:\findbugs-3.0.0
set PATH=%ANT_HOME%\bin;%JAVA_HOME%\bin;%FINDBUGS_HOME%\bin;
Dicek setelah di setting, hasilnya :
Eksekusi menggunakan Apache Ant
C:\>ant -version
Apache Ant(TM) version 1.9.4 compiled on April 29 2014
C:\>java -version
java version "1.8.0_20"
Java(TM) SE Runtime Environment (build 1.8.0_20-b26)
Java HotSpot(TM) Client VM (build 25.20-b23, mixed mode)
C:\>findbugs -version
3.0.0

Selanjutya Ketikan di Command Prompt :

C:\modul6>ant compile //untuk mengkompilasi tidak akan menghasilkak error
Output :
Buildfile: C:\modul7\build.xml
clean:
     [echo] Cleaning and creating new directory
   [delete] Deleting directory C:\modul7\classes
    [mkdir] Created dir: C:\modul7\classes
compile:
     [echo] compiling all vehicles and tests classes
    [javac] C:\modul7\build.xml:18: warning: 'includeantruntime' was not set, de
faulting to build.sysclasspath=last; set to false for repeatable builds
    [javac] Compiling 2 source files to C:\modul7\classes
    [javac] warning: [options] bootstrap class path not set in conjunction with
-source 1.5
    [javac] warning: [options] source value 1.5 is obsolete and will be removed
in a future release
    [javac] warning: [options] To suppress warnings about obsolete options, use
-Xlint:-options.
    [javac] 3 warnings
BUILD SUCCESSFUL
Total time: 4 seconds

C:\modul7>ant run // menjalan atau running program
Output:
Buildfile: C:\modul7\build.xml
clean:
     [echo] Cleaning and creating new directory
   [delete] Deleting directory C:\modul7\classes
    [mkdir] Created dir: C:\modul7\classes
compile:
     [echo] compiling all vehicles and tests classes
    [javac] C:\modul7\build.xml:18: warning: 'includeantruntime' was not set, de
faulting to build.sysclasspath=last; set to false for repeatable builds
    [javac] Compiling 2 source files to C:\modul7\classes
    [javac] warning: [options] bootstrap class path not set in conjunction with
-source 1.5
    [javac] warning: [options] source value 1.5 is obsolete and will be removed
in a future release
    [javac] warning: [options] To suppress warnings about obsolete options, use
-Xlint:-options.
    [javac] 3 warnings
run:
     [java] We have a new bicycle wth speed = 20, cadence = 10, gear = 1
BUILD SUCCESSFUL
Total time: 2 seconds

C:\modul7>ant findbugs //menfindbugs dan disimpan
Output:
Buildfile: C:\modul7\build.xml
clean:
     [echo] Cleaning and creating new directory
   [delete] Deleting directory C:\modul7\classes
    [mkdir] Created dir: C:\modul7\classes
compile:
     [echo] compiling all vehicles and tests classes
    [javac] C:\modul7\build.xml:18: warning: 'includeantruntime' was not set, de
faulting to build.sysclasspath=last; set to false for repeatable builds
    [javac] Compiling 2 source files to C:\modul7\classes
    [javac] warning: [options] bootstrap class path not set in conjunction with
-source 1.5
    [javac] warning: [options] source value 1.5 is obsolete and will be removed
in a future release
    [javac] warning: [options] To suppress warnings about obsolete options, use
-Xlint:-options.
    [javac] 3 warnings
findbugs:
 [findbugs] Executing findbugs FindBugsTask from ant task
 [findbugs] Running FindBugs...
 [findbugs] Calculating exit code...
 [findbugs] Exit code set to: 0
 [findbugs] Output saved to findbugs-results.txt
BUILD SUCCESSFUL
Total time: 5 seconds
