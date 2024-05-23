# Redeemer

Redeemer is a tech test. It's a fictional project where we want to allow users to create an account, redeem scratch codes, and see their redeemed codes. It's to get a familiarity with the t3 stack: typescript, tailwind, tRPC - the 3 "T's", as well as nextjs, react, prisma, planetscale and next-auth.

## Instructions

Get the base project up and running. FGirst, create a database on planetscale and plug the connection string into the .env file. Then follow [this guide](https://create.t3.gg/en/usage/first-steps) to get Prisma and next-auth authentication set up. I reccomend just using discord or github as the next-auth provider, as it's the easiest to set up.

Note take a look at the `src/env.js` file. This puts rules in place about the environment variables that are required. The app wont run until you meet those rules.

You'll notice in the `schema.prisma` file, there is a Post entity. This is just a placeholder, and you can delete it. You'll need to create a new entity for the scratch codes. The scratch code should have a string of 10 characters, which should be unique. Once you've configured that, run `npm run db:push` to update the planetscale database schema to reflect your new model.

Create a prisma seed file to populate a few scratch codes to the database. The prisma docs will help you here.

Update the homepage to fetch and display a serial code to ensure you have it all working. Once you've got that and auth working, you can start on the actual project.

Create a new page that allows users to redeem a scratch code. When a user redeems a scratch code, it should be added to their list of redeemed codes (if you havent already, you'll need to update the database schema to account for this relationship between serials and users). The api to redeem a code should return a 400 if the code is invalid (doesnt exist or is already redeemed), and a 200 if it's valid. Now update the homepage to show their redeemed codes.

## Bonus points (react state stuff)

To get familiarity with react state management, create a CodesProvider that wraps the entire app using react's `useContext`. This should provide the user's redeemed codes to the entire app (wrap your code in the _app.tsx file in the provider). This will allow you to remove the need to fetch the user's redeemed codes on the homepage, and instead have the code in the context provider wait until the user is available out of next-auth, then fetch the users redeemed codes from there, and expose them to any consumer of the CodesProvider.

On the homepage now you can just use your new context provider to show the user's redeemed codes if there are any, and notable, as the project expands, you can use this context provider to provide the user's redeemed codes to any page that need them.

Once that's working, update the redeem page to use the context provider to use react `useState` to track how many times they have tried to redeem a code. If they have tried and failed to redeem a code more than 3 times in a row, show a message saying they have tried too many times and to bugger off.

## General docs and resources

This is a [T3 Stack](https://create.t3.gg/) project bootstrapped with `create-t3-app`.

We try to keep this project as simple as possible, so you can start with just the scaffolding we set up for you, and add additional things later when they become necessary.

If you are not familiar with the different technologies used in this project, please refer to the respective docs. If you still are in the wind, please join our [Discord](https://t3.gg/discord) and ask for help.

- [Next.js](https://nextjs.org)
- [NextAuth.js](https://next-auth.js.org)
- [Prisma](https://prisma.io)
- [Tailwind CSS](https://tailwindcss.com)
- [tRPC](https://trpc.io)

To learn more about the [T3 Stack](https://create.t3.gg/), take a look at the following resources:

- [Documentation](https://create.t3.gg/)
- [Learn the T3 Stack](https://create.t3.gg/en/faq#what-learning-resources-are-currently-available) — Check out these awesome tutorials

You can check out the [create-t3-app GitHub repository](https://github.com/t3-oss/create-t3-app) — your feedback and contributions are welcome!

To deploy this, follow our deployment guides for [Vercel](https://create.t3.gg/en/deployment/vercel), [Netlify](https://create.t3.gg/en/deployment/netlify) and [Docker](https://create.t3.gg/en/deployment/docker) for more information.
