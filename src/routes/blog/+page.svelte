<script lang="ts">
	let idToken: string;
import { initializeApp } from "firebase/app";
import { getAuth, createUserWithEmailAndPassword } from "firebase/auth";
const firebaseConfig = {
  apiKey: import.meta.env.VITE_API_KEY,
  authDomain: import.meta.env.VITE_AUTH_DOMAIN,
  projectId: import.meta.env.VITE_PROJECT_ID,
  storageBucket: import.meta.env.VITE_STORAGE_BUCKET,
  messagingSenderId: import.meta.env.VITE_MESSEGING_SENDER_ID,
  appId: import.meta.env.VITE_APP_ID,
  measurementId: import.meta.env.VITE_MEASUREMENT_ID,
};
export function fbinitialize() {
  initializeApp(firebaseConfig);
}
fbinitialize();
export async function FireBaseSignIn()  {

  const auth = getAuth();
  const userCredential = await createUserWithEmailAndPassword(
    auth,
    'owatanbe26@gmail.com',
    'hogehoge'
  );
  const user = userCredential.user;
  idToken = await user.getIdToken();
  return idToken;
};

  </script>
  
  <button on:click={FireBaseSignIn}>データを取得</button>
  
  {#if idToken}
	<ul>
		<li>{idToken}</li>
	</ul>
  {/if}