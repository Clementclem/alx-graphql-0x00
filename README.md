GraphQuest: Exploring and Implementing GraphQL


Objective: Learners will write a GraphQL query to retrieve a specific character’s information using their ID.

Use the following Endpoint

Objective: Learners will create a GraphQL query to retrieve a paginated list of all characters.

Instructions:

Write a GraphQL query using the characters(page: Int) field to fetch the list of characters. For page 1, 2, 3, 4
Select the subfields: id, name, status, and image.


Objective: Learners will write a GraphQL query to fetch the details of a specific episode using its ID.

Instructions:

Write a GraphQL query using the episode(id: ID!) field to retrieve details of an episode.
Include the following fields in your query: id, name, air_date, episode 

Objectives: To kickstart the development of your rick and morty application using Next.js, you will set up a new project with TypeScript, ESLint, and Tailwind CSS.

Instructions:

Create a project alx-rick-and-morty-app in alx-graphql-0x01 directory
Change directory into alx-rick-and-morty-app
Install the following dependencies:

npm install @apollo/client graphql
npm install @types/graphql
Create an empty directory named: ‘graphql’ in your root directory
Create an empty file apolloClient.ts under graphql directory
Replace the content of the file with the follow:

import { ApolloClient, InMemoryCache, HttpLink} from "@apollo/client"

const client = new ApolloClient({
  link: new HttpLink({
    uri: "https://rickandmortyapi.com/graphql"
  }),
  cache: new InMemoryCache()
})

export default client;
Create an empty file queries.ts under graphql directory
Replace the content of the file with the follow:
import { gql } from "@apollo/client";

export const GET_EPISODES = gql`
  query getEpisodes($page: Int, $filter: FilterEpisode) {
    episodes(page: $page, filter: $filter) {
      info {
        pages
        next
        prev
        count
      }
      results {
        id
        name
        air_date
        episode
      }
    }
  }
`;
Open your _app.tsx file located under pages directory

Replace the content with the follow:

import "@/styles/globals.css";
import type { AppProps } from "next/app";
import { ApolloProvider } from "@apollo/client";
import client from "@/graphql/apolloClient";

export default function App({ Component, pageProps }: AppProps) {
  return (
    <ApolloProvider client={client}>
      <Component {...pageProps} />
    </ApolloProvider>
  )
}
Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000 to see the changes made.



Objectives: Learn to query the Rick and Morty GraphQL endpoint to retrieve data about episodes.

Instructions:

Duplicate alx-graphql-0x01 to alx-graphql-0x02
Change directory to alx-rick-and-morty-app
Create an empty directory named: interfaces under the root directory
Create an empty file name: index.ts under the interfaces directory
Replace the content with the follow:
interface InfoProps {
    pages: number
    next: number
    prev: number
    count: number
}

export interface EpisodeProps {
  id: number
  name: string
  air_date: string
  episode: string
  info: InfoProps
}

export type EpisodeCardProps = Pick<EpisodeProps, 'id' | 'name'| 'air_date' | "episode">
Open your index.tsx file located under pages directory
Replace the content with the follow:
import { useQuery } from "@apollo/client"
import { GET_EPISODES } from "@/graphql/queries"
import { EpisodeProps } from "@/interfaces"
import EpisodeCard from "@/components/common/EpisodeCard"
import { useEffect, useState } from "react"



const Home: React.FC = () => {

  const [page, setPage] = useState<number>(1)
  const { loading, error, data, refetch } = useQuery(GET_EPISODES, {
    variables: {
      page: page
    }
  })

  useEffect(() => {
    refetch()
  }, [page, refetch])

  if (loading) return <h1>Loading...</h1>
  if (error) return <h1>Error</h1>

  const results = data?.episodes.results
  const info = data?.episodes.info

  return (
    <div className="min-h-screen flex flex-col bg-gradient-to-b from-[#A3D5E0] to-[#F4F4F4] text-gray-800">
      {/* Header */}
      <header className="bg-[#4CA1AF] text-white py-6 text-center shadow-md">
        <h1 className="text-4xl font-bold tracking-wide">Rick and Morty Episodes</h1>
        <p className="mt-2 text-lg italic">Explore the multiverse of adventures!</p>
      </header>

      {/* Main Content */}
      <main className="flex-grow p-6">
        <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
          {results && results.map(({ id, name, air_date, episode }: EpisodeProps, key: number) => (
            <EpisodeCard
              id={id}
              name={name}
              air_date={air_date}
              episode={episode}
              key={key}
            />
          ))}
        </div>

        {/* Pagination Buttons */}
        <div className="flex justify-between mt-6">
          <button 
            onClick={() => setPage(prev => prev > 1 ? prev - 1 : 1)}
            className="bg-[#45B69C] text-white font-semibold py-2 px-6 rounded-lg shadow-lg hover:bg-[#3D9B80] transition duration-200 transform hover:scale-105">
            Previous
          </button>
          <button 
            onClick={() => setPage(prev => prev < info.pages ? prev + 1 : prev)}
            className="bg-[#45B69C] text-white font-semibold py-2 px-6 rounded-lg shadow-lg hover:bg-[#3D9B80] transition duration-200 transform hover:scale-105">
            Next
          </button>
        </div>
      </main>

      {/* Footer */}
      <footer className="bg-[#4CA1AF] text-white py-4 text-center shadow-md">
        <p>&copy; 2024 Rick and Morty Fan Page</p>
      </footer>
    </div>
  )
}

export default Home
Create the following file components/common/EpisodeCard.tsx

Replace the content of the file with the follow:

import { EpisodeCardProps } from "@/interfaces";

const EpisodeCard = ({ id, name, air_date, episode }: EpisodeCardProps) => {
  return (
    <div key={id} className="bg-white cursor-pointer shadow-md rounded-lg p-4 m-4 transition-transform duration-200 hover:scale-105">
      <div className="flex justify-between items-center">
        <h2 className="text-xl font-semibold text-gray-800">{name}</h2>
        <span className="border px-2 text-xs rounded-full bg-blue-600 text-white flex items-center">{episode}</span>
      </div>
      <p className="text-gray-600">{air_date}</p>
    </div>
  );
};

export default EpisodeCard;
Save and close your files
Run npm run dev from the terminal
From a tab in your browser type http://localhost:3000 to see the changes made.
