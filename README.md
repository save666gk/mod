from news.models import *

Создать двух пользователей (с помощью метода User.objects.create_user).
user01 = User.objects.create(username = 'User01Name', first_name = 'Daniil') user02 = User.objects.create(username = 'User02Name', first_name = 'Sanya')

user01 = User.objects.get(id=1) user02 = User.objects.get(id=2)

Создать два объекта модели Author, связанные с пользователями.
author01 = Author.objects.create(authorUser = user01) author02 = Author.objects.create(authorUser = user02)

author01 = Author.objects.get(id=1) author02 = Author.objects.get(id=2)

Добавить 4 категории в модель Category.
category01 = Category.objects.create(name='АЙТИ') category02 = Category.objects.create(name='Спорт') category03 = Category.objects.create(name='наука') category04 = Category.objects.create(name='Космос')

category01 = Category.objects.get(id=1) category02 = Category.objects.get(id=2) category03 = Category.objects.get(id=3) category04 = Category.objects.get(id=4)

Добавить 2 статьи и 1 новость.
article01 = Post.objects.create(author=author01, kindCategory='AR', title='Заголовок_статьи_1', text='Текст_статьиt_1') article02 = Post.objects.create(Author=author01, kindCategory='AR' , title='Заголовок_статьи_2', text='Текст_статьиt_2')

news01 = Post.objects.create(postAuthor=author02, kindCategory='NW', title='Заголовок_новости_1', text='Текст_новости_1')

article01 = Post.objects.get(id=1) article02 = Post.objects.get(id=2)

news01 = Post.objects.get(id=3)

Присвоить им категории (как минимум в одной статье/новости должно быть не меньше 2 категорий).
article01.postCategory.add(category01) article01.postCategory.add(category02) article02.postCategory.add(category03)

news01.postCategory.add(category03)

Создать как минимум 4 комментария к разным объектам модели Post (в каждом объекте должен быть как минимум один комментарий).
comment01 = Comment.objects.create(commentPost=article01, commentUser=user01, Text='Текст_статьи_комментария_1') comment02 = Comment.objects.create(commentPost=article02, commentUser=user02, Text='Текст_статьи_комментария_2') comment03 = Comment.objects.create(commentPost=article01, commentUser=user01, Text='Текст_статьи_комментария_3') comment04 = Comment.objects.create(commentPost=news01, commentUser=user02, Text='Текст_новости_комментария_1')

comment01 = Comment.objects.get(id=1) comment02 = Comment.objects.get(id=2) comment03 = Comment.objects.get(id=3) comment04 = Comment.objects.get(id=4)

Применяя функции like() и dislike() к статьям/новостям и комментариям, скорректировать рейтинги этих объектов.
comment01.like() comment02.like() comment03.like() comment04.like() comment01.like() comment02.like() comment03.like() comment01.like() comment02.like() comment01.like() comment01.dislike() comment04.dislike() comment03.dislike() comment01.dislike() article01.like() article01.like() article01.like() article01.like() article01.like() article02.like() article02.like() article02.like() news01.dislike()

Обновить рейтинги пользователей.
author01.update_rating() author02.update_rating()

посмотрели рейтинг автора
author01.ratingAuthor author02.ratingAuthor

Вывести username и рейтинг лучшего пользователя (применяя сортировку и возвращая поля первого объекта).
best = Author.objects.all().order_by('-ratingAuthor').values('authorUser', 'ratingAuthor')[0]

print(best)

Вывести дату добавления, username автора, рейтинг, заголовок и превью лучшей статьи, основываясь на лайках/дислайках к этой статье.
Post.objects.all().order_by('-rating').values('dateCreation', 'Author__authorUser__username', 'rating', 'title', 'text')[0]

Вывести все комментарии (дата, пользователь, рейтинг, текст) к этой статье.
Comment.objects.all().order_by().values('dateCreation', 'commentUser__username', 'commentPost', 'rating', 'Text')[0]




Post.objects.all().values('postAuthor', 'title') Post.objects.filter(author=author02) Post.objects.filter(title='Заголовок_статьи_1').values('author')

Comment.objects.all().values('commentPost', 'commentUser') Comment.objects.filter(commentPost=article01).values('Text') Comment.objects.filter(commentText='Текст_статьи_комментария_2').values('rating')

Author.objects.filter(id=1) Author.objects.all().values('authorUser', 'id')
