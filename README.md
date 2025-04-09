# gramin--connect-app// App.js
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import HomeScreen from './screens/HomeScreen';
import GaonItihas from './screens/GaonItihas';
import ShikayatForm from './screens/ShikayatForm';
import ChatScreen from './screens/ChatScreen';
import ECommerce from './screens/ECommerce';
import TeamForm from './screens/GramKhelLeague/TeamForm';
import Fixtures from './screens/GramKhelLeague/Fixtures';
import Leaderboard from './screens/GramKhelLeague/Leaderboard';

const Tab = createBottomTabNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator screenOptions={{ headerShown: true }}>
        <Tab.Screen name="होम" component={HomeScreen} />
        <Tab.Screen name="इतिहास" component={GaonItihas} />
        <Tab.Screen name="शिकायत" component={ShikayatForm} />
        <Tab.Screen name="चैट" component={ChatScreen} />
        <Tab.Screen name="ई-मार्केट" component={ECommerce} />
        <Tab.Screen name="टीम पंजीकरण" component={TeamForm} />
        <Tab.Screen name="मैच" component={Fixtures} />
        <Tab.Screen name="अंक तालिका" component={Leaderboard} />
      </Tab.Navigator>
    </NavigationContainer>
  );// firebaseConfig.js
import { initializeApp } from 'firebase/app';
import { getFirestore } from 'firebase/firestore';
import { getAuth } from 'firebase/auth';

const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "your-project.firebaseapp.com",
  projectId: "your-project-id",
  storageBucket: "your-project.appspot.com",
  messagingSenderId: "your-messaging-id",
  appId: "your-app-id"
};

const app = initializeApp(firebaseConfig);
export const db = getFirestore(app);
export const auth = getAuth(app);
}GraminConnect/
├── App.js
├── firebaseConfig.js
├── screens/
│   ├── HomeScreen.js
│   ├── GaonItihas.js
│   ├── ShikayatForm.js
│   ├── ChatScreen.js
│   ├── ECommerce.js
│   └── GramKhelLeague/
│       ├── TeamForm.js
│       ├── Fixtures.js
│       └── Leaderboard.js# Gramin Connect – Powered by Kumar Harshit Singh Ji (Semaria, Bihar)

## उद्देश्य:
भारत के गाँवों को तकनीक से जोड़ने वाला पहला ऐप – इतिहास, पंचायत, शिकायत, चैट, खेल, और मार्केटिंग – सब एक जगह।

## उपयोग:

1. Firebase Console पर नया Project बनाएँ
2. firebaseConfig.js में अपनी Firebase details भरें
3. React Native CLI या Expo से `npm install` करें
4. `npm start` या `expo start` से ऐप चलाएँ
5. APK बनाने के लिए Android Studio का उपयोग करें

---

### सम्मानपूर्वक समर्पित:  
**Kumar Harshit Singh Ji (18 वर्ष)  
सेमरिया हवेली, नरौणी वंश, सीवान, बिहार**// HomeScreen.js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

const HomeScreen = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Gramin Connect</Text>
      <Text style={styles.subtitle}>Powered by Kumar Harshit Singh Ji</Text>
    </View>
  );
};

export default HomeScreen;

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  title: {
    fontSize: 26,
    fontWeight: 'bold',
  },
  subtitle: {
    fontSize: 16,
    marginTop: 10,
  },
});// GaonItihas.js
import React from 'react';
import { ScrollView, Text, StyleSheet } from 'react-native';

const GaonItihas = () => {
  return (
    <ScrollView style={styles.container}>
      <Text style={styles.heading}>सेमरिया गाँव का इतिहास</Text>
      <Text style={styles.text}>
        बाबू रामअवतार सिंह जी सेमरिया के पहले निर्विरोध मुखिया थे। उन्होंने ज़मीन दान दी और अंग्रेजों की अधीनता नहीं मानी।
        वे नरौणी वंश के गौरव थे, जिनका स्वर्णकाल आज भी लोगों के दिलों में बसता है...
      </Text>
    </ScrollView>
  );
};

export default GaonItihas;

const styles = StyleSheet.create({
  container: {
    padding: 20,
  },
  heading: {
    fontSize: 22,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  text: {
    fontSize: 16,
    lineHeight: 22,
  },
});// GaonItihas.js
import React from 'react';
import { ScrollView, Text, StyleSheet } from 'react-native';

const GaonItihas = () => {
  return (
    <ScrollView style={styles.container}>
      <Text style={styles.heading}>सेमरिया गाँव का इतिहास</Text>
      <Text style={styles.text}>
        बाबू रामअवतार सिंह जी सेमरिया के पहले निर्विरोध मुखिया थे। उन्होंने ज़मीन दान दी और अंग्रेजों की अधीनता नहीं मानी।
        वे नरौणी वंश के गौरव थे, जिनका स्वर्णकाल आज भी लोगों के दिलों में बसता है...
      </Text>
    </ScrollView>
  );
};

export default GaonItihas;

const styles = StyleSheet.create({
  container: {
    padding: 20,
  },
  heading: {
    fontSize: 22,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  text: {
    fontSize: 16,
    lineHeight: 22,
  },
});// ShikayatForm.js
import React, { useState } from 'react';
import { View, TextInput, Button, StyleSheet, Text, Alert } from 'react-native';
import { db } from '../firebaseConfig';
import { collection, addDoc } from 'firebase/firestore';

const ShikayatForm = () => {
  const [shikayat, setShikayat] = useState('');

  const handleSubmit = async () => {
    if (shikayat.trim() === '') return Alert.alert('कृपया शिकायत लिखें');
    await addDoc(collection(db, 'shikayatein'), { text: shikayat });
    Alert.alert('शिकायत दर्ज हो गई');
    setShikayat('');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.label}>अपनी शिकायत दर्ज करें:</Text>
      <TextInput
        style={styles.input}
        multiline
        numberOfLines={4}
        value={shikayat}
        onChangeText={setShikayat}
        placeholder="यहाँ लिखें..."
      />
      <Button title="सबमिट करें" onPress={handleSubmit} />
    </View>
  );
};

export default ShikayatForm;

const styles = StyleSheet.create({
  container: {
    padding: 20,
  },
  label: {
    fontSize: 18,
    marginBottom: 10,
  },
  input: {
    borderWidth: 1,
    borderColor: '#888',
    marginBottom: 15,
    padding: 10,
    borderRadius: 5,
  },
}); // ChatScreen.js
import React, { useState, useEffect } from 'react';
import { View, TextInput, Button, FlatList, Text, StyleSheet } from 'react-native';
import { db } from '../firebaseConfig';
import { collection, addDoc, onSnapshot, query, orderBy } from 'firebase/firestore';

const ChatScreen = () => {
  const [msg, setMsg] = useState('');
  const [messages, setMessages] = useState([]);

  useEffect(() => {
    const q = query(collection(db, 'chats'), orderBy('timestamp', 'desc'));
    const unsubscribe = onSnapshot(q, (snapshot) => {
      setMessages(snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
    });
    return () => unsubscribe();
  }, []);

  const handleSend = async () => {
    if (msg.trim() === '') return;
    await addDoc(collection(db, 'chats'), {
      text: msg,
      timestamp: new Date(),
    });
    setMsg('');
  };

  return (
    <View style={styles.container}>
      <FlatList
        data={messages}
        inverted
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => <Text style={styles.message}>{item.text}</Text>}
      />
      <TextInput
        style={styles.input}
        value={msg}
        onChangeText={setMsg}
        placeholder="संदेश लिखें..."
      />
      <Button title="भेजें" onPress={handleSend} />
    </View>
  );
};

export default ChatScreen;

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 10,
  },
  input: {
    borderWidth: 1,
    padding: 8,
    marginTop: 5,
    marginBottom: 10,
  },
  message: {
    padding: 8,
    borderBottomWidth: 1,
    borderColor: '#ccc',
  },
}); // ECommerce.js
import React, { useState } from 'react';
import { View, TextInput, Button, FlatList, Text, StyleSheet } from 'react-native';
import { db } from '../firebaseConfig';
import { collection, addDoc, getDocs } from 'firebase/firestore';

const ECommerce = () => {
  const [product, setProduct] = useState('');
  const [products, setProducts] = useState([]);

  const addProduct = async () => {
    if (product.trim() === '') return;
    await addDoc(collection(db, 'products'), { name: product });
    setProduct('');
    fetchProducts();
  };

  const fetchProducts = async () => {
    const querySnapshot = await getDocs(collection(db, 'products'));
    setProducts(querySnapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>ग्राम मार्केट</Text>
      <TextInput
        style={styles.input}
        value={product}
        onChangeText={setProduct}
        placeholder="नया उत्पाद जोड़ें"
      />
      <Button title="जोड़ें" onPress={addProduct} />
      <FlatList
        data={products}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => <Text style={styles.item}>{item.name}</Text>}
      />
    </View>
  );
};

export default ECommerce;

const styles = StyleSheet.create({
  container: { padding: 20 },
  title: { fontSize: 20, fontWeight: 'bold', marginBottom: 10 },
  input: { borderWidth: 1, marginBottom: 10, padding: 8 },
  item: { padding: 8, borderBottomWidth: 1 },
});// TeamForm.js
import React, { useState } from 'react';
import { View, TextInput, Button, Alert, StyleSheet } from 'react-native';
import { db } from '../../firebaseConfig';
import { collection, addDoc } from 'firebase/firestore';

const TeamForm = () => {
  const [team, setTeam] = useState('');

  const handleAdd = async () => {
    if (team.trim() === '') return Alert.alert('टीम का नाम डालें');
    await addDoc(collection(db, 'teams'), { name: team });
    Alert.alert('टीम पंजीकृत हो गई');
    setTeam('');
  };

  return (
    <View style={styles.container}>
      <TextInput
        placeholder="टीम का नाम"
        value={team}
        onChangeText={setTeam}
        style={styles.input}
      />
      <Button title="पंजीकरण करें" onPress={handleAdd} />
    </View>
  );
};

export default TeamForm;

const styles = StyleSheet.create({
  container: { padding: 20 },
  input: { borderWidth: 1, padding: 10, marginBottom: 10 },
}); // Fixtures.js
import React, { useEffect, useState } from 'react';
import { View, FlatList, Text, StyleSheet } from 'react-native';
import { db } from '../../firebaseConfig';
import { collection, getDocs } from 'firebase/firestore';

const Fixtures = () => {
  const [matches, setMatches] = useState([]);

  const fetchMatches = async () => {
    const snapshot = await getDocs(collection(db, 'fixtures'));
    setMatches(snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
  };

  useEffect(() => {
    fetchMatches();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>मैच सूची</Text>
      <FlatList
        data={matches}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <Text style={styles.item}>
            {item.team1} vs {item.team2} — {item.date}
          </Text>
        )}
      />
    </View>
  );
};

export default Fixtures;

const styles = StyleSheet.create({
  container: { padding: 20 },
  title: { fontSize: 20, fontWeight: 'bold' },
  item: { padding: 10, borderBottomWidth: 1 },
});// Leaderboard.js
import React, { useEffect, useState } from 'react';
import { View, FlatList, Text, StyleSheet } from 'react-native';
import { db } from '../../firebaseConfig';
import { collection, getDocs } from 'firebase/firestore';

const Leaderboard = () => {
  const [teams, setTeams] = useState([]);

  const fetchTeams = async () => {
    const snapshot = await getDocs(collection(db, 'leaderboard'));
    setTeams(snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() })));
  };

  useEffect(() => {
    fetchTeams();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>अंक तालिका</Text>
      <FlatList
        data={teams}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <Text style={styles.item}>{item.name} - {item.points} अंक</Text>
        )}
      />
    </View>
  );
};

export default Leaderboard;

const styles = StyleSheet.create({
  container: { padding: 20 },
  title: { fontSize: 20, fontWeight: 'bold' },
  item: { padding: 10, borderBottomWidth: 1 },
});
