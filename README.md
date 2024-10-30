# React Flow Org Chart Example by @randomdrake

👋 Hello! Welcome to a little proof of concept I put together to showcase and practice skills with:

* TypeScript
* JavaScript
* JSX
* React
* Tailwind
* React Flow
* Vite

This is a straightforward fake org chart generator. It does the following:

* Creates a fake org chart given the number of employees
* Lets you draw org charts vertically or horizontally
* Creates realistic-ish looking organizations with a CEO on the top, managers beneath, and teams of 1-7 people underneath them
* Uses [Faker](https://github.com/faker-js/faker) to generate names, titles, and profile images
* Utilizes [React Flow](https://reactflow.dev/) and the [Dagre](https://github.com/dagrejs/dagre)

## Running the App
`npm install` - Install the dependencies

`npx tailwindcss -i ./src/input.css -o ./public/output.css --watch` - Build the Tailwind CSS

`npm run dev` - Run the program using Vite

## Screenshots
Horizontal Layout

![Horizontal Layout](https://github.com/randomdrake/react-flow-org-chart/blob/main/public/screenshot-horizontal.png?raw=true)

Vertical Layout

![Vertical Layout](https://github.com/randomdrake/react-flow-org-chart/blob/main/public/screenshot-vertical.png?raw=true)

Detail

![Vertical Layout](https://github.com/randomdrake/react-flow-org-chart/blob/main/public/screenshot-detail.png?raw=true)