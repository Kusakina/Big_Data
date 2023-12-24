В данной лабораторной работе необходимо было познакомиться с архитектурой и принципами работы zookeeper. Выполнить задания:
Решить проблему обедающих философов (каждый философ - отдельный процесс в системе)
Реализовать двуфазный коммит протокол для high-available регистра (каждый регистр - отдельный процесс в системе)
с использованием Zookeeper сервиса.

# Ход работы:
1. Ознакомиться с Zookeeper, работая в консоли.

2. Реализуем двуфазный коммит протокол
Потоки разделяются на два типа: Coordinator и Worker.
В CoordinatorЕ создается эфимерный узел, далее следует ожидание голосов от WorkerОВ (commit - если worker готов к работе и abort - если не готов, commit и abort задаются рандомно),
как только число голосов равно числу WorkerОВ, Coordinator выдает сообщение о том, что получены все голоса.
Worker создает эфимерный узел дочерний к узлу координатора, с соответствующим ответом (commit или abort).
Далее Coordinator подсчитывает голоса для каждого варианта (commit, abort), в зависимости от того, каких голосов больше принимает решение.
После принятия решения  Coordinator рассылает его дочерним узлам ( WorkerАМ).

3. Решаем задачу с обедающими философами:
Пять философов располагаются за круглым столом.
Философ может размышлять или кушать. 
Для приема пищи в центре стола большое блюдо с неограниченным количеством спагетти и тарелки, по одной перед каждым философом.
Поесть спагетти можно только с использованием двух вилок. Для этого на столе располагается ровно пять вилок – по одной между тарелками философов.

Для решения создадим массив вилок-семафоров. 
Каждый философ сначала берет левую вилку, затем – правую, принимает пище, кладет правую вилку, затем – левую и прекращает прием пищи, начинает размышления.
Для того, чтобы избежать ситуации, в которой все философы взяли по левой вилке и ждут (блокировка), для 0 философа сменим порядок, в котором он берет вилки.
Теперь нулевой философ начинает прием пищи с поднятия правой вилки.

Результат программы:

  1. Philosopher 0 is going to eat
  2. Philosopher 4 is going to eat
  3. Philosopher 1 is going to eat
  4. Philosopher 2 is going to eat
  5. Philosopher 3 is going to eat
  6. Philosopher 2 picked up the left fork
  7. Philosopher 4 picked up the left fork
  8. Philosopher 3 picked up the left fork
  9. Philosopher 1 picked up the left fork
  10. Philosopher 4 picked up the right fork
  11. Philosopher 4 put the right fork
  12. Philosopher 4 put the loft fork and finished eating
  13. Philosopher 3 picked up the right fork
  14. Philosopher 4 is thinking
  15. Philosopher 4 is going to eat
  16. Philosopher 3 put the right fork
  17. Philosopher 4 picked up the left fork
  18. Philosopher 3 put the loft fork and finished eating
  19. Philosopher 2 picked up the right fork
  20. Philosopher 4 picked up the right fork
  21. Philosopher 3 is thinking
  22. Philosopher 2 put the right fork
  23. Philosopher 2 put the loft fork and finished eating
  24. Philosopher 1 picked up the right fork
  25. Philosopher 2 is thinking
  26. Philosopher 3 is going to eat
  27. Philosopher 3 picked up the left fork
  28. Philosopher 2 is going to eat
  29. Philosopher 4 put the right fork
  30. Philosopher 4 put the loft fork and finished eating
  31. Philosopher 3 picked up the right fork
  32. Philosopher 4 is thinking
  33. Philosopher 1 put the right fork
  34. Philosopher 2 picked up the left fork
  35. Philosopher 1 put the loft fork and finished eating
  36. Philosopher 0 picked up the right fork
  37. Philosopher 1 is thinking
  38. Philosopher 0 picked up the left fork
  39. Philosopher 1 is going to eat
  40. Philosopher 3 put the right fork
  41. Philosopher 3 put the loft fork and finished eating
  42. Philosopher 2 picked up the right fork
  43. Philosopher 3 is thinking
  44. Philosopher 0 put the right fork
  45. Philosopher 1 picked up the left fork
  46. Philosopher 0 put the loft fork and finished eating
  47. Philosopher 0 is thinking
  48. Philosopher 2 put the right fork
  49. Philosopher 2 put the loft fork and finished eating
  50. Philosopher 1 picked up the right fork
  51. Philosopher 2 is thinking
  52. Philosopher 0 is going to eat
  53. Philosopher 1 put the right fork
  54. Philosopher 1 put the loft fork and finished eating
  55. Philosopher 0 picked up the right fork
  56. Philosopher 1 is thinking
  57. Philosopher 0 picked up the left fork
  58. Philosopher 0 put the right fork
  59. Philosopher 0 put the loft fork and finished eating
  60. Philosopher 0 is thinking
  61. Process finished with exit code 0


