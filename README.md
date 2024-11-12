  # understandJvm
 //Класс JvmComprehension загружается через подсистему загрузчиков классов - ClassLoaders, где ищется данный
//класс по очереди на 3-х уровнях: bootstrap, platform, application. Если класс находится на каком-то из уровней,
//то происходит его загрузка, также предварительно осуществляется его проверка на то, что код валиден, подготовка
// примитивов статических полей, связывание ссылок на другие классы(если есть).
// Данные об этом классе перемещаются для хранения в metaspace.

public class JvmComprehension {

    public static void main(String[] args) {
        //В стэк формируется фрейм main
        int i = 1;                      // 1 во фрейме main создается переменная  i, значение которой = 1
        Object o = new Object();        // 2 переменная о создается в стэке фрейма main и хранит в себе ссылку на объект
                                        // new Object  - новый объект создается для хранения в heap.
        Integer ii = 2;                 // 3 поскольку Integer является ссылочной переменной, то переменная ii
                                        // помещается в стэк main и хранит в себе ссылку на значение объекта Integer,
                                        //само значение объекта создается для хранения в heap.
        printAll(o, i, ii);             // 4 в стэке формируется фрейм printAll, далее см. комментарий в п. 4.1 .
                                        //o и ii cодержат ссылку на объекты
        System.out.println("finished"); // 7 в стэке формируется фрейм println, в котором создается ссылка на объект
                                        // String, значение которого "finished". Сам же объект типа String со значением
                                        // создается для хранения в хипе.
    }
    // Код программы выполняется строка за строкой, каждый метод компиляруется по очереди в машинный код, интерпритатор
    // интерпретирует машинный код строка за строкой, затем выполняет. Периодически сборщик мусора собирает объекты,
    // которые больше не используются, из памяти путем обхода графа достижимых объектов. Обычно при сборке мусора
    //приостанавливается работа всей программы.

    private static void printAll(Object o, int i, Integer ii) { //4.1 во фрейме printAll(в стэке) создаются переменные o
        //и ii, которые содержат ссылку на объекты Object o и Integer ii в хипе, а также в стэке создается переменная
        //i со значением 1
        Integer uselessVar = 700;                   // 5 в стэке во фрейме printAll для хранения создается  переменная
                                                    // uselessVar, которая хранит в себе ссылку на объект Integer. Сам
                                                    // объект со значением 700 хранится в хипе .
        System.out.println(o.toString() + i + ii);  // 6 в стэке фомируется фреймы println и toString. В фрейм println
        //передаются переменные i со значением 1, ii, o, последние из которых хранят ссылки на объекты
        // Object o, Integer ii.
    }
}
