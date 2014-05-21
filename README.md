Руководство по установке/запуску

1) git clone https://github.com/railstutorial/sample_app_rails_4.git - клонируем проект
2) $ cd sample_app_rails_4 - переходим в папку
3) $ cp config/database.yml.example config/database.yml - делаем свой файл конфигурации БД
4) $ bundle install --without production - синхронизируем гемы
5) $ bundle exec rake db:migrate - запускаем миграции
6) $ bundle exec rake db:test:prepare - подготавливаем тестовую БД
7) $ bundle exec rspec spec/ - запускаем тесты
8) Во первых ставим imagemagick: 
brew install imagemagick
9) Прописываем гем: gem "paperclip", "~> 4.1"
10) Добавляем в файл модели:

has_attached_file :avatar, :styles => { :medium => "300x300>", :thumb => "100x100>" }

validates_attachment_content_type :avatar, :content_type => /\Aimage\/.*\Z/

11) Создаем миграции:
  def self.up
    add_attachment :users, :avatar
  end

  def self.down
    remove_attachment :users, :avatar
  end
  
12) Добавляем в форму: <%= form.file_field :avatar %>

13) В users_controller:
private

def user_params
  params.require(:user).permit(:avatar)
end

14) В users_helper добавляем метод avatar_url который возвращает картинку с аватаром нужного размера
