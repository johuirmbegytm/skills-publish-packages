<header>

<!--
  <<< Author notes: Course header >>>
  Include a 1280×640 image, course title in sentence case, and a concise description in emphasis.
  In your repository settings: enable template repository, add your 1280×640 social image, auto delete head branches.
  Add your open source license, GitHub uses the MIT license.
-->

# Publish to GitHub Packages

_Use GitHub Actions to publish your project to a Docker image._

</header>

<!--
  <<< Author notes: Step 4 >>>
  Start this step by acknowledging the previous step.
  Define terms and link to docs.github.com.
-->

## Step 4: Pull your image

_Now things are running! :sparkles:_

Whoa, now things are running! This may take a few minutes. This might take a tiny amount of time, so grab your popcorn :popcorn: and wait for the build to finish before moving on.

:cook: While we wait for the build to finish, let's take care of a few prerequisites.

For ease of use and cross-platform compatibility (Windows, Mac, and Linux), we'll focus on Docker Desktop. Not to be confused, Docker Engine is the foundation for running containers while **[Docker Desktop](https://www.docker.com/blog/how-to-check-docker-version/)** bundles Docker Engine, a GUI, and a Virtual Machine in a _single installation_.

1. Install [Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/#install-docker-desktop-on-windows).
   * If you're using Mac or Linux, locate the correct install steps at the previous link via the lefthand tree menu.
1. Open Docker Desktop and [briefly explore](https://docs.docker.com/desktop/use-desktop/).
1. For running `docker` commands, access the command-line terminal either via Bash, Git Bash, Windows Command Prompt or PowerShell.

:inbox_tray: To pull the Docker image, we need to log into Docker first.

Before we can use this Docker image, you will need to generate a [personal access token (classic)](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) that contains the following permissions:

**Scopes for Personal Access Token (classic)** :coin:
- repo (all)
- write:packages
- read:packages

![screenshot personal access token creation page with boxes for repo (all), write:packages, and read:packages checked](https://user-images.githubusercontent.com/3250463/219254714-82bb1da5-33b1-491b-97c0-b25f51494f6a.png)

We will use this token to log in to Docker, and authenticate with the package.

1. Open your terminal (Bash or Git Bash recommended).
1. Use the following command to log in:
   ```bash
   docker login ghcr.io -u USERNAME
   ```
1. Replace `USERNAME` with your GitHub username.
1. Enter your new Personal Access Token as the password.
1. Press **Enter**.

If everything went well, :crossed_fingers: you should see `Login Succeeded` in your terminal.

### :keyboard: Activity: Pull your image

1. Copy the `pull` command from the package instructions.
   - :fire: _Tip: To reach this page, click the **Code** tab at the top of your repository. Then, find the navigation bar below the repository description, and click the **Packages** heading link_
     ![screenshot of the pull command on the GitHub package page](https://user-images.githubusercontent.com/3250463/219254981-9ff949fa-4d01-46e3-9e3d-b8ce3710c2a9.png)
   - Or alternatively, in the following URL replace `YOURNAME`, `REPONAME`, and browse to `https://github.com/users/YOURNAME/packages?repo_name=REPONAME` and click on the package name
1. Replace `YOURNAME` with your GitHub username.
1. Replace `TAG` with the image tag.
1. Paste the `pull` command into your terminal. It should look something like this:
   - `docker pull ghcr.io/YOURNAME/publish-packages/game:TAG`
1. Press **Enter**.
1. You should see output indicating that the pull was successful, like `Status: Downloaded newer image for ghcr.io/YOURNAME/publish-packages/game:TAG`.
   ![screenshot of successful Docker image output](https://user-images.githubusercontent.com/3250463/219255178-3c943a6f-6c15-4f59-9002-228249b1c469.png)
1. _We can't automatically verify this step for you, so please continue on to the next step below!_
<!--
  <<< Author notes: Step 5 >>>
  Start this step by acknowledging the previous step.
  Define terms and link to docs.github.com.
-->

## Step 5: Run your image

_Nicely done grabbing your Docker image! :relaxed:_

Let's trying running it.

### :keyboard: Activity: Run your image

1. Find your image information by typing `docker image ls`.
   ![screenshot of output from Docker image ls command: lists docker images, REPOSITORY TAG and docker URL](https://i.imgur.com/UAwRXiq.png)<!-- This screenshot should be changed. -->
1. Use the following command to run a container from your image:
   ```bash
   docker run -dp 8080:80 --rm <YOUR_IMAGE_NAME:TAG>
   ```
1. Replace `YOUR_IMAGE_NAME` with your image name under the `REPOSITORY` column.
1. Replace `TAG` with the image tag under the `TAG` column.
1. Press **Enter**.
1. If everything went well, you will see hash value as output on your screen.
1. Optionally, you can open [localhost:8080](http://localhost:8080) to see the page you just created.
1. _We can't automatically verify this step for you, so please continue on to the next step below!_
<!--
  <<< Author notes: Finish >>>
  Review what we learned, ask for feedback, provide next steps.
-->

## Finish

_Congratulations friend, you've completed this course!_

<img src=https://octodex.github.com/images/collabocats.jpg alt=celebrate width=300 align=right>

Here's a recap of all the tasks you've accomplished in your repository:

- You wrote a workflow that sends a code through a continuous delivery pipeline.
- You built a fully deployable artifact.
- You did so using GitHub Actions and GitHub Packages!

### What's next?

- Publish your own packages from your projects.
- We'd love to hear what you thought of this course [in our discussion board](https://github.com/orgs/skills/discussions/categories/publish-packages).
- [Take another GitHub Skills course](https://github.com/skills).
- [Read the GitHub Getting Started docs](https://docs.github.com/en/get-started).
- To find projects to contribute to, check out [GitHub Explore](https://github.com/explore).

<footer>

<!--
  <<< Author notes: Footer >>>
  Add a link to get support, GitHub status page, code of conduct, license link.
-->

---

Get help: [Post in our discussion board](https://github.com/orgs/skills/discussions/categories/publish-packages) &bull; [Review the GitHub status page](https://www.githubstatus.com/)

&copy; 2023 GitHub &bull; [Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

</footer>

# Лабораторна-практична робота №11

## Тема:

Автоматизація збірки та публікації Docker-образів у GitHub Packages за допомогою GitHub Actions.

## Мета:

Навчитися налаштовувати процес безперервної доставки (CD) для пакування застосунку в Docker-образ, автоматичної публікації його у GitHub Container Registry (GHCR) та подальшого розгортання локально.

### Хід роботи:

#### 1.	Підготовка репозиторію та робочої гілки

На основі шаблону `skills/publish-packages` було створено новий публічний репозиторій `skills-publish-packages`. Для виконання завдання було обрано гілку `cd`, у якій проводилася розробка конфігураційних файлів.

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/1.png?raw=true>)

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/2.png?raw=true>)

#### 2.	Створення Workflow-файлу для CD

У директорії `.github/workflows/` було створено файл `publish.yml`. У конфігурації було налаштовано тригер на `push` у гілку `main`, а також визначено необхідні права доступу (`packages: write`) для завантаження образів у реєстр.

Ключові параметри файлу:

- `images`: `ghcr.io/johuirmbegytm/publish-packages/game` — шлях до сховища образу.
- `tags`: `type=sha` — автоматичне маркування образу унікальним хешем комміту.
- `steps`: використання готових екшенів для логіну (`login-action@v3`) та збірки образу (`build-push-action@v5`).

```bash
name: Publish to Docker
on:
  push:
    branches:
      - main
permissions:
  packages: write
  contents: read
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Docker meta
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ghcr.io/johuirmbegytm/publish-packages/game
          tags: type=sha

      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.repository_owner }}
          password: ${{ secrets.GITHUB_TOKEN }}

      - name: Build container
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
```

#### 3.	Створення Dockerfile

Для збірки образу в корінь проєкту було додано `Dockerfile`. Він базується на сервері `nginx:1.24-alpine` та копіює статичні файли гри (`Tic Tac Toe`) у стандартну директорію сервера.

```bash
FROM nginx:1.24-alpine
COPY . /usr/share/nginx/html
```


#### 4.	Злиття змін та запуск конвеєра

Було створено `Pull Request` для злиття гілки `cd` з `main`. Після підтвердження злиття (`Confirm merge`) `GitHub Actions` автоматично запустив процес збірки.
Результати збірки в `Actions`:
- Успішна авторизація в `GitHub Container Registry`.
- Збірка образу (`Build container`).
- Публікація образу в розділ `Packages` репозиторію.

#### 5.	Авторизація та завантаження образу локально

Для перевірки опублікованого пакета було згенеровано `Personal Access Token` (`PAT`) з правами `write:packages` та `read:packages`.

1. `Login`: Виконано авторизацію в терміналі через команду 

```bash
docker login ghcr.io -u johuirmbegytm
```

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/3.png?raw=true>)

2. `Pull`: Завантажено створений образ на локальну машину: 

```bash
docker pull ghcr.io/johuirmbegytm/publish-packages/game:sha-00f341e
```

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/4.png?raw=true>)

#### 6.	Запуск та тестування застосунку

Завантажений образ було запущено локально за допомогою команди: 

```bash
docker run -dp 8080:80 --rm ghcr.io/johuirmbegytm/publish-packages/game:sha-00f341e
```

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/5.png?raw=true>)

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/6.png?raw=true>)

Після запуску застосунок `Tic Tac Toe` став доступним у браузері за адресою `localhost:8080`. Гра працює коректно, що підтверджує правильність збірки образу та налаштування сервера `Nginx`.

>![placeholder](<https://github.com/johuirmbegytm/skills-publish-packages/blob/main/images/7.png?raw=true>)
