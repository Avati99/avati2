import { Canvas, useFrame } from '@react-three/fiber';
import { useRef } from 'react';
import * as THREE from 'three';
import { TextureLoader } from 'three';
import { useLoader } from '@react-three/fiber';

const AnimatedPlane = ({ texture }) => {
    const meshRef = useRef();

    useFrame(({ clock }) => {
        if (meshRef.current) {
            meshRef.current.rotation.y = Math.sin(clock.getElapsedTime()) * 0.5;
        }
    });

    return (
        <mesh ref={meshRef}>
            <planeGeometry args={[5, 3]} />
            <meshBasicMaterial map={texture} />
        </mesh>
    );
};

const Scene = () => {
    const texture = useLoader(TextureLoader, 'your_image_url_here'); // Заменить на URL извлеченного кадра

    return (
        <Canvas>
            <ambientLight intensity={0.5} />
            <pointLight position={[10, 10, 10]} />
            <AnimatedPlane texture={texture} />
        </Canvas>
    );
};

export default Scene;
