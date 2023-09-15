# Django_lab2

cd NewsPaper
	
from news.models import *

1.Создать двух пользователей (с помощью метода User.objects.create_user('username')):

	User.objects.create_user('Bob') 
	User.objects.create_user('Sara') 
	User.objects.create_user('Samuel') 

2.Создать два объекта модели Author, связанные с пользователями:

	alan = User.objects.create_user('Alan')   
	Author.objects.create(user=alan) 
	barbara = User.objects.create_user('Barbara')
	Author.objects.create(user=barbara)  

3.Добавить 4 категории в модель Category:

	Category.objects.create(name='Sport')
	Category.objects.create(name='Cinema')
	Category.objects.create(name='Fashion')
	Category.objects.create(name='Politic')

//создаем соответствующие переменные категорий:
	sport = Category.objects.get(name='Sport')
	cinema = Category.objects.get(name='Cinema')
	fashion = Category.objects.get(name='Fashion')
	politic = Category.objects.get(name='Politic')

4,5.Добавить 2 статьи и 1 новость, присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий):
	
	author_alan = Author.objects.get(user=alan)
	Post.objects.create(author=author_alan, post_type='article', text = 'Мода и спорт на протяжении  тесно пересекаются и тренды в одном неизбежно приводят к изменениям в другом. Много одежды, становившейся популярной в разные времена, пришло из определенного вида спорта. Даже женские брюки, без которых сейчас сложно представить гардероб современной девушки, пришли из атлетики, так как активные упражнения в юбках выполнять было невозможно. Из зимних видов в повседневную жизнь пришли зимние и осенние куртки из мембраны и материала Softshell. Благодаря отличному функционалу этих материалов, они отлично проявляют себя в разных регионах страны, их выбирают взрослые и дети. В детской одежде популярными становятся мембранные комбинезоны, которые можно носить ранней осенью или при сильных морозах, в зависимости от утеплителя. В связи с возрастающей популярностью, производители одежды для спорта изготавливают комбинезоны и куртки ярких расцветок и интересного дизайна, чтобы все больше')
	article_1 = Post.objects.get(pk=1)
	article_1.categories.add(sport)
	article_1.categories.add(fashion)

	author_barbara = Author.objects.get(user=barbara)
	Post.objects.create(author=author_barbara, post_type='article', text='По стремительности глобальных перемен, сменяемости кадров, на которых фиксируется внимание зрителя и которые презентуют новые стандарты политической культуры, прошедшее столетие справедливо сравнить с кино. Хотя между мировым кинематографом и мировой политикой существует сложная взаимосвязь, она не позволяет называть кинематограф зеркалом политики')
	article_2 = Post.objects.get(pk=2)
	article_2.categories.add(cinema)
	article_2.categories.add(politic)

	Post.objects.create(author=author_alan, post_type='article', text = 'Спортивный скаут Стэнли Шугерман (Адам Сэндлер) вечно пропадает в командировках в поисках молодых и перспективных баскетболистов. Наконец, в Испании он находит талантливого спортсмена, которому приходится работать на стройке и кормить семью. Шугерман уговаривает парня прилететь в США и пройти драфт в НБА. Не подведёт ли баскетболист скаута?')
	article_3 = Post.objects.get(pk=3)
	article_3.categories.add(sport)
	article_3.categories.add(cinema)

6.Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).

//создаем соотетствующие переменные пользователей:	
	alan = User.objects.get(username='Alan')
	barbara = User.objects.get(username='Barbara')
	bob = User.objects.get(username='Bob')
	sara = User.objects.get(username='Sara')
	samuel = User.objects.get(username='Samuel')

// генерируем комментарии:
	Comment.objects.create(post=article_1, user=barbara, text='Nice article')
	Comment.objects.create(post=article_1, user=bob, text='Really Nice article')
	Comment.objects.create(post=article_2, user=sara, text='Not bad')
	Comment.objects.create(post=article_3, user=samuel, text='I appritiate for this')
	
7. Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов:
	
	article_1.like()
	article_1.like()
	article_1.like()
	article_1.dislike()

	article_2.like()
	article_2.like()
	article_2.dislike()

	article_3.like()

// создаем соответствующие переменные коментариев:
	comm_1 = Comment.objects.get(pk=1)
	comm_2 = Comment.objects.get(pk=2)
	comm_3 = Comment.objects.get(pk=3)
	comm_4 = Comment.objects.get(pk=4)

//генерируем лайки/дизлайки:
	comm_1.like()
	comm_1.like()
	comm_1.like()
	
	comm_2.dislike()

	comm_3.like()
	
	comm_4.like()

8. Обновить рейтинги пользователей:
	
Вариант 1
	пример для автора с именем Alan:

	1)создание переменной пользователя Alan:
		alan = User.objects.get(username='Alan') 
	2)создание переменной автора Alan:
		author_alan = Author.objects.get(user=alan)
	3)получение суммарного рейтинга каждой статьи автора умножается на 3:
		author_alan.get_author_posts_rate()
	4)получение суммарного рейтинга всех комментариев автора:
		author_alan.get_author_comments_rate()
	5)получение суммарного рейтинга всех комментариев к статьям автора:
		author_alan.get_comments_to_author_posts_rate()
	6)обновление рейтинга автора:
		author_alan.update_rating(сумма рейтингов полученных выше)
__________________________________________________________________________________

Вариант 2:

	1)Раскоментируйте метод update_rating() класса Author строка 33-34 и закоментируйте метод update_rating() строка 30-31 в файле models.py
	
	2)Перезагрузите консоль командой: 
		python manage.py shell
 	3)создание переменной пользователя Alan:
		alan = User.objects.get(username='Alan') 
	4)создание переменной автора Alan:
		author_alan = Author.objects.get(user=alan)
	5)обновление рейтинга автора:
		author_alan.update_rating()

*Подобные действия следует провести для всех авторов (в нашем случае для Barbara) для наполнения поля rate в экземплярах класса Author

9. Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта):

	best_author = Author.objects.order_by('-rate').first()
	best_author.user
	best_author.rate

10. Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье:
	
	best_post = Post.objects.order_by('-rate').first()
	best_post.date
	best_post.author.user
	best_post.title
	best_post.preview()
	
	
11.Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье:
	
	Получение обьекта всех комментраиев к посту:
		comments_to_best_post = Comment.objects.filter(post=best_post)
____________________________________________________________________________________________
Вариант 1: Реализовать функцию вида:

	def get_comments_to_post(some_post): // передаем в аргумент экземпляр класса Post (в нашем случае переменная best_post из п. 10)
		for comment in Comment.objects.filter(post=some_post):
			for value in comment:
				print(value)
___________________________________________________________________________________________
Вариант 2:
	Перегрузить (переопределить) метод строкового представления объекта Comment __str__():
		def __str__(self):
		    return (f'Дата:{self.date}, пользователь:{self.user}, рейтинг: {self.rate}, текст: {self.text}')

	Таким образом при вызове функции вида:
		print(Comment.objects.filter(post=best_post).first()) -> строковое представление вида: <дата:значение, пользователь:значение, рейтинг:значение, текст:значение> для отдельного комментария к этой статье		
	
